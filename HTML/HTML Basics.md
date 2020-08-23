# HTML Basics

**Hyper**

- 텍스트 등의 정보가 동일 선상에 있는 것이 아니라 다중으로 연결되어 있는 상태

**Hyper Text**

- 참조(하이퍼링크)를 통해 사용자가 한 문서에서 다른 문서로 즉시 접근 할 수 잇는 텍스트
- 하이퍼 텍스트가 쓰인 기술등 중 가장 중요한 2가지 (http, html)

**Markup Language**

- 특정 텍스트에 역할을 부여하는, 따라서 "마크업을 한다" 라고 하는 건 제목이 제목이라하고 본문이 본문이라고 마킹을 하는 것
- ex) h1 tag는 단순히 글자가 커지는 것이 아니라 의미론적으로 그 페이지에서 가장 핵심 주제를 의미하는 것

## HTML

- 웹 페이지를 작성하기 위한(구조를 잡기 위한) 언어
- 웹 컨텐츠의 의미와 구조를 정의
- `.html` 형태

<br>

## HTML Element의 구조

![img](img/grumpy-cat-small.png)

- Opening & Closing tag : 요소의 시작과 끝을 나타냄
- Content: Element의 내용물 (예시의 경우 단순 텍스트)

<br>

### Block VS Inline Elements

- **Block-level element**: Creates a literal **block** on the page. 기본적으로 가로폭 전체의 넓이를 가지는 직사각형 형태가 되며 줄바꿈이 자동으로 이뤄짐. 블록 요소는 모든 인라인 요소를 포함할 수 있고 다른 블록 요소도 일부 포함 할 수 있음

  - `article`, `div`, `footer`, `form`, `h1, h2 ...`, `header`, `hr`, `ol`, `p`, `section`, `table`, `ul` ...
  
- **Inline element**: 항상 블록 요소안에 포함되어 있으며 인라인 요소안에 다른 인라인 요소가 포함될 수 있음. 기본적으로 컨텐츠가 끝나는 지점까지를 넓이로 가지게 됨. 인라인 뒤에는 줄바꿈이 없고 바로 이어서 다음 요소가 올 수 있음

  - `a`, `b`, `br`, `button`, `em`, `img`, `label`, `script`, `span`, `textarea` ...

<br>

## Attributes(속성)
![grumpy-cat](img/grumpy-cat-attribute-small.png)

- 태그의 부가적인 정보 표시
- 태그와 상관없이 사용 가능한 속성들(html global attribute)도 있음

<br>

## HTML 문서의 구조

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>My test page</title>
  </head>
  <body>
    <p>This is my page</p>
  </body>
</html>
```

- `<!DOCTYPE html>`: 이 문서는 HTML 형식임! 유효하다고 알려주는 정도
- `<html>` : HTML 문서의 최상위 요소로 문서의 root를 뜻함. `head`와 `body` 부분으로 구분됨
- `<head>`: 페이지 이용자에게는 보이지 않지만 검색 결과에 노출 될 키워드, 웹페이지 설명, CSS 스타일, 인코딩 등 HTML 페이지의 모든 내용을 담고 있음
- `<meta charset="utf-8">`: (=Open Graph Protocol) HTML 문서의 메타 데이터를 통해 문서의 정보를 전달. 페이스북에서 만들었으며, 메타정보에 해당하는 제목, 설명 문자 인코딩 설정 등을 슬 수 있도록 정의
- `<title>`: 브라우저 탭에 표시되는 페이지 제목
- `<body>`: 브라우저 화면에 나타나는 정보로 실제 내용에 해당

<br>

### DOM(Document Object Model)

웹 페이지가 로딩될 때 브라우저는 아래와 같은 HTML DOM을 내부적으로 생성함

![DOM HTML tree](img/pic_htmltree.gif)

HTML DOM은 Object들의 tree 형태로 만들어짐. Javascript는 HTML DOM을 참조하여 HTML 요소를 추가하거나 삭제하고 스타일을 변경할 수 있게 됨

**HTML DOM**

- DOM은 문서의 구조화된 표현(structured representation)을 제공하며 프로그래밍 언어가 DOM 구조에 접근할 수 있는 방법을 제공함으로써 문서 구조, 스타일, 내용 등을 변경할 수 있게 도움
- HTML 요소들을 **객체**로 표현 = 웹 페이지의 객체 지향 표현