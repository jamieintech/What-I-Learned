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

