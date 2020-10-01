# Upload images with Django

> CRUD 게시판에서 글도 쓰고 이미지도 첨부할 수 있게 해보자

## MEDIA

Media in Django indicates files that are uploaded by users (a.k.a 첨부파일) 

By default, Django stores files locally using the *MEDIA_ROOT* and *MEDIA_URL* settings

### Media_ROOT

- absolute filesystem path to the directory that will hold user-uploaded files
  - 유저가 업로드한 파일을 배치할 최상위 경로 지정 (어디에 파일이 저장되게 할 것인가?)

```python
# settings.py

# 이 프로젝트의 'media'라는 폴더를 미디어 최상위 경로로 지정
MEDIA_ROOT = BASE_DIR / 'media'
```

### Media_URL

- 업로드된 파일의 주소(URL)를 만들어 주는 역할
- `/`이 필수이고 문자열로 설정해야한다
- 일반적으로 `/media`를 사용

```python
# settings.py

# 파일 주소를 만들때 앱/media/파일이름 형식으로 만들어달라!
MEDIA_URL = '/media/'
```

### 이미지 경로 설정

> :exclamation:주의: 장고에서 **개발**단계와 **배포**단계의 차이가 좀 많이남. 지금 설정하는건 다 **개발**단계!

방금 *MEDIA_ROOT*와 *MEDIA_URL*을 통해서 **개발단계**에서 유저가 올린 이미지를 내 프로젝트(crud)의 **media**라는 폴더로 업로드 할 수 있게 설정했다

이제 이미지를 로컬 환경의 프로젝트 폴더 안에 저장시킬 수는 있는데, 이걸 READ하면서 불러올 때는 `url`을 통해서 불러와야함 ==> **프로젝트**의 **urls.py**에서 미디어를 가져오고 저장시킬건지 알려줘야함

#### urls.py 

```python
# crud > urls.py

# media import용
from django.conf import settings            # 이건 내 settings 불러오는거
from django.conf.urls.static import static  # 이건 static한 파일(media)를 주소로 불러오기 위해

urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/', include('articles.urls')),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

- `settings.MEDIA_URL` : 어떤 미디어 url을 정적으로 추가할지
- `document_root=settings.MEDIA_ROOT` : 실제 해당 미디어 파일은 어디에 있는지
- `article.image.url` == `/media/이미지이름.jpg`

<br>

## Image Field

유저가 이미지를 업로드할 수 있도록 만들어보자

먼저 *Article* 모델에 새로운 필드를 추가한다

```python
# articles > models.py

class Article(models.Model):
	...
    # 이미지
    # blank=True : permit empty values in forms()
    image = models.ImageField(blank=True)
```

:exclamation: 참고로 이미지필드를 추가하기 전 `pip install Pillow`가 필수다

추가사항에 대해서 `makemigrations`를 해주고, Pillow가 있는지 확인 후 `migrate`를 해준다. 이제 `runserver`를 해서 새 글 작성하는 페이지에 가보면 이미지를 올리수 있는 첨부파일 칸이 생긴 것을 확인할 수 있다

<br>

## CREATE

미디어 파일은 form을 통해 받을 수 있도록 **인코딩**을 해줘야한다

#### new.html

```django
<form action="{% url 'articles:create' %}" method="POST" enctype="multipart/form-data">
  {% csrf_token %}
  {{form.as_p}}
  <input type="submit">
</form>
```

- `enctype` : 인코딩 타입
- `multipart/form-data` : POST 형식으로 파일 전송을 할 수 있게끔 해주는 인코딩 타입

#### views.py

```python
def create(request):
    # CRUD 연습이랑 코드 동일
    if request.method == 'POST':
        
        # form에 파일도 받기!!!! POST로 파일도 왔으니 그것도 받으라고 알려주기
        form = ArticleForm(request.POST, request.FILES)
        if form.is_valid():
            article.save()
            return redirect('articles:detail', article.pk)
    else: 
        form = ArticleForm()
    context = {
        'form': form,
    }
    return render(request, 'articles/create.html', context)
```

이미지를 올렸을 때 내 프로젝트 > media안에 잘 있는지 확인해보자

<br>

## READ

올린 이미지를 불러와보자

#### detail.html

```django
<!-- 이미지 태그 추가 -->
<img src="{{article.image.url}}" alt="{{article.image}}">
```

- `article.image.url` - 파일의 주소
- `article.image` - 파일 이름

이렇게하면 **이미지가 있는 게시글**은 잘 나오는데, 문제는 이미지가 없는 게시글이다! (에러가 떠버림..) if문을 통해 이미지 있으면 불러오고 없으면 안불러오는 식으로 처리해버리자

```django
{% if article.image %}
<img src="{{article.image.url}}" alt="{{article.image}}">
{% endif %}
```

<br>

## UPDATE

이미지는 바이너리 데이터(하나의 덩어리)라서 텍스트처럼 *일부만 수정 하는게 불가능*하다. 그렇기 때문에 `Input value` 에 넣어서 수정하는 방식을 사용하는 게 아니고, 새로운 사진으로 덮어 씌우는 방식을 사용한다

아무튼 딱히 바꿀거는 update.html에서 `enctype="multipart/form-data"` 추가해주고 `def update`에서 ArticleForm을 받을 때 `request.FILES`도 같이 받는 것!

<br>

## 이미지 업로드 경로 수정

위에서 처음 설정한 이미지 업로드 경로는 *내 프로젝트 > media*폴더

하지만 이대로라면 하나의 폴더에 모든 이미지가 업로드돼서 나중에 관리하기가 어려워진다. 이를 위해 해결할 수 있는 2가지 방법!

1. 날짜로 분류해보기

   > https://docs.python.org/3/library/time.html#time.strftime

   ```python
   # models.py
   
   class Article(models.Model):
       title = models.CharField(max_length=20)
       content = models.TextField()
       image = models.ImageField(blank=True, upload_to='%Y/%m/%d/')
       created_at = models.DateTimeField(auto_now_add=True)
       updated_at = models.DateTimeField(auto_now=True)
   ```

   ```bash
   $ python manage.py makemigrations
   $ python manage.py migrate
   ```

2. FileField에 정의된 모델 인스턴스 사용 (이건 유저 필요)

   ```python
   # models.py
   
   def articles_image_path(instance, filename):
       return f'user_{instance.user.pk}/{filename}'
   
   class Article(models.Model):
       title = models.CharField(max_length=20)
       content = models.TextField()
       image = models.ImageField(blank=True, upload_to=articles_image_path)
       created_at = models.DateTimeField(auto_now_add=True)
       updated_at = models.DateTimeField(auto_now=True)
   ```

   ```bash
   $ python manage.py makemigrations
   $ python manage.py migrate
   ```

   - `instance` --> instance는 Article 모델의 객체
   - `filename` --> 업로드한 이미지 파일의 이름


## Image Resizing

이미지를 업로드 할때부터 사이즈 조절하기!

:exclamation:참고로 `django-imagekit` 설치 후 진행해야함 (INSTALLED_APPS에 'imagekit' 추가)

내가 원하는 사이즈의 썸네일 형태로 원본이미지를 조정한 후 저장하는 방법

#### models.py

```python
# image resizing
from imagekit.models import ProcessedImageField
from imagekit.processors import Thumbnail

class Article(models.Model):
	
    image = ProcessedImageField(
        blank=True,
        processors=[Thumbnail(200,300)],
        format='JPEG',
        options={'quality':90},
    )

```

`ProcessedImageField()`의 parameter로 들어가 있는 값들은 makemigrations 후에 변경이 되더라도 **다시 makemigrations 를 해줄 필요 없다** (개꿀)

<br>

### libraries

- `Pillow` 

  - Pillow는 PIL 프로젝트에서 fork 되어서 나온 라이브러리. 
  - PIL이 Python3를 지원하지 않기 때문에 Pillow를 많이 씀.(`ImageField()` 사용시에 필수 라이브러리)

- `pilkit`

  - Pillow를 쉽게 쓸 수 있도록 도와주는 라이브러리. 다양한 Processors 지원
  - https://github.com/matthewwithanm/pilkit/tree/master/pilkit/processors
  - Thumbnail
  - Resize
  - Crop

- `django-imagekit`

  - 이미지 썸네일 helper Django 앱(실제 이미지를 처리할 때는 Pilkit을 사용)
  - 이미지 썸네일 helper 장고 앱


