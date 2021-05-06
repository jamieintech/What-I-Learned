# HTTP Protocol

HTTP (Hypertext Transfer Protocol)는 웹 서버와 웹 클라이언트 사이에서 데이터를 주고받기 위해 사용하는 통신 방식이다.

> Protocol : a system of rules that define how data is exchanged within or between computers (=통신 규격)

Hypertext 전송용 protocol로 시작했지만, 이제는 HTML이나 XML 등의 하이퍼텍스트뿐만 아니라 이미지, 음성, 동영상, 자바스크립트, pdf 등 컴퓨터에서 다룰 수 있는 데이터라면 무엇이든 전송할 수 있다.



<br>

### 웹 프로그래밍이란?

HTTP(S)로 통신하는 클라이언트와 서버를 개발하는 것이다.

![http](img/http.png)

웹 클라이언트가 웹 서버에 HTTP 요청(**= request**) 메세지를 보내면 웹 서버가 요청에 응답한 결과를 HTTP 응답(**= response**) 메세지로 보낸다.

이런 방식으로 request와 response가 반복적으로 오가면서 웹을 사용할 수 있게 된다. 

> generally, a web client == web browser

<br>

### HTTP 처리 방식

HTTP method를 통해서 클라이언트가 원하는 처리 방식을 서버에 알려줄 수 있다. 

주요 HTTP method 4 가지는 데이터 조작의 기본이 되는 CRUD와 매핑되는 처리를 한다.

| 메소드명 |           의미            | CRUD와 매핑되는 역할 |
| :------: | :-----------------------: | :------------------: |
|   GET    | 존재하는 자원에 대한 요청 |         Read         |
|   POST   |    새로운 자원을 생성     |        Create        |
|   PUT    | 존재하는 자원에 대한 변경 |        Update        |
|  DELETE  | 존재하는 자원에 대한 삭제 |        Delete        |

<br>

#### GET & POST

HTML의 `<form>`에서 지정할 수 있는 메소드가 GET과 POST밖에 없기 때문에 이 두 가지를 가장 많이 사용한다. 

- **GET**: URL에서 `?` 뒤에 `key=value` 형태로 데이터 전송
  - `https://docs.djangoproject.com/en/3.1/search/?q=form`
- **POST**: GET에서 URL에 포함시켰던 파라미터들을 request message의 바디에 넣어서 URL에는 생략 가능
  - `https://docs.djangoproject.com/en/3.1/ref/forms/`

