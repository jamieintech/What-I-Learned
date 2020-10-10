# AUTH login with Django

>  쟹고로 로그인 기능 구현하기~~~
>
> 기본 CRUD가 되는 crud/articles 프로젝트에 추가적으로 유저를 만들어봅시다

## Accounts

회원가입 및 로그인 기능을 위해 유저들을 만들어보자. 장고에서 auth 관련 기본 설정들은 다 **accounts**라는 이름으로 설정돼있기 때문에 이왕이면 accounts로 app을 만든다

```bash
$ py manage.py startapp accounts
```

새 앱을 만들었으니 해야할 일

1. settings.py에 앱 등록
2. 프로젝트의 urls.py에 path추가해주기
3. 새로 만든 앱(accounts) 안에 urls.py 만들기

<br>

## Sign up

장고에서 기본적으로 제공하는 `UserCreationForm`을 사용해서 신규 유저를 받아보자. 기본적으로 게시글 Create하는 거랑 거의 똑같음. 일단 회원가입할 수 있는 페이지로 이동하는 것만 (GET)만 해보자

#### urls.py

```python
# accounts > urls.py

app_name = 'accounts'

urlpatterns = [
    path('signup/', views.signup, name='signup'),   
]
```

### views.py

```python
from django.shortcuts import render, redirect

# 장고에서 제공하는 회원가입폼
from django.contrib.auth.forms import UserCreationForm

def signup(request):
    if request.method == 'POST':
        form = UserCreationForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('articles:index')

    else: 
        form = UserCreationForm()
    context = {
        'form': form
    }
    return render(request, 'accounts/signup.html', context)
```

### signup.html

```django
{% extends 'base.html' %}

{% block content %}

<b>sign up</b>

<form action="{% url 'accounts:signup' %}" method="post">
  {% csrf_token %}
  {{form.as_p}}
  <input type="submit" value="sign up">
</form>

{% endblock content %}
```

이제 runserver를 해보면 내가 회원가입 폼을 만들지도 않았는데!! 유저 모델을 만들지도 않았는데!! 회원가입이 된다!!! admin페이지에 가면 확인 가능!

<br>

## Login

회원가입에는 `UserCreationForm`이 있었다. 로그인에는 `AuthenticationForm`이 있다! 회원가입과 로그인 기능을 제공하다니...쟹고 짱...

### urls.py

```python
path('login/', views.login, name='login'), 
```

### views.py

```python
from django.shortcuts import render, redirect
from django.contrib.auth.forms import UserCreationForm, AuthenticationForm
from django.contrib.auth import login as auth_login

def login(request):
    if request.method == 'POST':
        # request가 먼저오고 그 다음에 request.POST
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            
            # django에서 제공하는 login기능으로 지금 입력된 유저 정보가 있는지만 확인하는거!
            auth_login(request, form.get_user())
            return redirect('articles:index')
    else:
        form = AuthenticationForm()
    context = {
        'form':form
    }
    return render(request, 'accounts/login.html', context)
```

<br>

## Logout

로그아웃은 현재 있는 세션을 삭제하는 방식이다

### views.py

```python
from django.contrib.auth import login as auth_login, logout as auth_logout

def logout(request):
    auth_logout(request)
    return redirect('articles:index')
```

장고의 auth에서 기본적으로 제공하는 `logout()`은 호출된 순간 현재 request에 대한 db의 session data를 완전히 정리하고, 클라이언트 쿠키에서도 sessionid가 삭제된다

<br>

## 로그인 접근 제한

로그인 했을 때는 회원가입/로그인 버튼이 안보이고 로그아웃 버튼만 보여야한다. 로그인 한 회원인지 확인하기 위해 `is_authenticated`를 사용하자

```django
<!-- base.html -->
<div class="navbar-nav ml-auto">
    
<!-- check if the current user in request's data authenticated -->
{% if request.user.is_authenticated %}
	<span class="nav-link disabled">Hello, {{user.username}}</span>
	<form action="{% url 'accounts:logout' %}" method="post">
		{% csrf_token %}
		<button type="submit" class="btn btn-link text-muted">LOGOUT</button>
	</form>

{% else %}
	<a class="nav-link" href="{% url 'accounts:signup' %}">SIGNUP</a>
	<a class="nav-link" href="{% url 'accounts:login' %}">LOGIN</a>
{% endif %}
</div>
```

장고 템플릿 태그의 if-else를 사용해서 nav bar에 로그인 후 회원가입/로그인 버튼이 안뜨게 처리했다. 하지만 아직 주소창에 직접 치면 접근은 가능하다! 이를 해결하기위해 `is_authenticated`를 `views.py`에서 처리해준다

### views.py

```python
# accounts > views.py

# 기존의 코드 위에 if문으로 유저 확인하기
def signup(request):
    if request.user.is_authenticated:
        return redirect('articles:index')

def login(request):
    if request.user.is_authenticated:
        return redirect('articles:index')
```

<br>

## login_required decorator

"새글 작성" 버튼도 nav bar에서 똑같이 if문을 걸어줘서 create/로 넘어가는 버튼이 안보이게 할 수 있다. 하지만 이래도 주소창에 create/를 치면 로그인을 안해도 새 글을 작성할 수 있게 된다. 이런걸 방지 하기 위해 무조건 로그인을 해야 특정 주소로 넘어갈 수 있도록 설정을 해보자

### views.py

```python
# accounts > views.py
from django.contrib.auth.decorators import login_required

@login_required
def create(request):

  
@login_required
def update(request, pk):

  
@login_required
def delete(request, pk):
```

이렇게 해두면 로그인이 안된 상태에서 해당 url을 주소창에 입력해서 강제로 접속하려 할때 `accounts/login`이 자동 소환(?)된다.

근데 이렇게 새로 소환된 주소창을 잘 보면 좀 이상하다

`http://127.0.0.1:8000/accounts/login/?next=/articles/create/` 이건 또 뭐여!

<br>

## "next" query string parameter

`@login_required` 은 기본적으로 **인증 성공 후 사용자를 리다이렉트 할 경로**를 **next **라는 스트링 파라미터 변수에 **저장**한다.

우리가 url 로 접근하려고 했던 그 주소가 로그인이 되어있지 않으면 볼 수 없는 곳이라서, django 가 로그인 페이지로 강제로 돌려 보냈는데, 로그인을 다시 정상적으로 하면 원래 요청했던 주소로 보내 주기 위해 **keep 해주는 것**이다 (그니까 지금은 로그인 안됐으니 로그인 페이지를 보여주고, 이거 후에! 이동할 주소가 next=에 포함된 것이다)

따로 처리 해주지 않으면 우리가 view에 설정한 redirect 경로로 이동하지만, next 에 저장된 주소로 이동되도록 만들기 위해 작업을 해보자.

### views.py

```python
def login(request):

    if request.user.is_authenticated:
        return redirect('articles:index')

    if request.method == 'POST':
        # request가 먼저오고 그 다음에 request.POST
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            auth_login(request, form.get_user())
            return redirect(request.GET.get('next') or 'articles:index')
```

