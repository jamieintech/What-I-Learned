# Managing static files in Django

> how to manage static files in Django!



## Static Files

- A static file content will be sent to the client (usually a browser) as it is without server intervention

  - CSS, JavaScript, and images are examples of static files
  - these files are not "generated" as they're loaded

  > By contrast, a dynamic file is parsed by the server which then renders a new set of data based on the dynamic file template. 
  
- Django provides `django.contrib.staticfiles` to help manage the static files
  - django에는 기본적으로 static의 위치가 `app_name/static/`으로 설정돼있다

    ```python
    # settings.py
    INSTALLED_APPS = [
        ...
        django.contrib.staticfiles	#기본적으로 추가되어 있음
    ]
    
    STATIC_URL = '/static/'			#기본적으로 맨 아래 추가되어 있음
    ```

<br>

## Configuring static files in Django

> There probably will be static files for each different app. Therefore it will be inefficient to have all your static files in a single folder called "static" under the app

### STATIC_ROOT

- the absolute path to the directory where collectstatic will collect static file routes for deployment

  > collectstatic: 프로젝트 배포 시 흩어져있는 static file들을 모아서 특정 디렉토리로 옮김
  >
  > 하나의 프로젝트에서 사용하는 정적 파일들은 여기저기에 분산되어 있기 때문에 요청이 들어왔을 때 필요한 정적 파일을 돌려주려면 많은 경로들을 다 찾아보아야 하며 이는 매우 비효율적일 것이다.
  >
  > 그래서 사용하는 모든 정적 파일을 하나의 경로로 모아주는 작업이 필요하다.
  > `runserver` 는 개발자가 개발에만 집중할 수 있도록 이 작업을 알아서 해준다. runserver는 알게모르게 알아서 해주는 편의기능이 아주 많다.
  > 하지만 실제 서비스를 배포할때는 runserver를 사용하지 않으므로 직접 모아주어야 하며, 이 때 사용하는 것이 `collectstatic` 명령이다.

### STATIC_URL

- URL to use when referring to sttaic files located in `STATIC_ROOT`

### STATICFILES_DIR

- default: empty list [ ]

- defines the additional locations of static files

- `crud/static/stylesheets` 에 `styles.css` 파일을 생성해서 링크를 설정 해보자. 이 

  #### settings.py

  ```python
  # settings.py 하단
  
  # Static files (CSS, JavaScript, Images)
  # https://docs.djangoproject.com/en/3.1/howto/static-files/
  
  # 각 app들의 static 폴더위주로 찾아보라고 기본 설정이 되어 있음
  STATIC_URL = '/static/'
  
  # 앱이 많거나 앱 밖에도 static폴더가 있으니 그것도 꼭 포함해서 확인하라고 알려주기
  # 아래는 base.html에 적용시킬 static 위치
  STATICFILES_DIRS = [
      BASE_DIR / 'crud' / 'static', 
  ]
  ```

  #### base.html

  ```django
  <!-- base.html -->
  
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  
    <!-- bootstrap-->
    {% bootstrap_css %}
  
    <!-- crud / static / stylesheets -->
    {% load static %}
    <link rel="stylesheet" href="{% static 'stylesheets/styles.css' %}">
    
    
  </head>
  ```

  static을 불러올 때는 불러온다고 알려줄 수 있는 `{% load static %}`추가가 필수임! 이거 없으면 못찾는다고 에러남

  static 폴더 만들기는 각 **앱 > static > 앱 이름 > staticfile.css** 이런식으로! templates처럼!

