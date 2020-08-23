# CSS 단위

> CSS 단위에는 absolute 단위와 relative 단위 두 종류로 나뉘지만 다양한 화면단에 적절하게 나타낼 때는 relative 단위가 더 많이 쓰임



## (상대) 크기 단위

**px**

- 모니터 해상도의 한 화소인 '픽셀'을 기준
- 픽셀의 크기는 변하지 않기 때문에 고정적인 단위

**%**

- 백분율 단위
- 가변적인 레이아웃에서 자주 사용

**em**

- em은 상속의 영향 받음, rem은 최상위 요소(html)를 기준으로 결정됨.
- 상황에 따라 각기 다른 값을 가질 수 있음 (relative to the font-size of the element)
  -  2em = current font size * 2

**rem**

- 최상위 요소인 `<html>`(root em)을  절대 단위를 기준으로 삼음. 상속의 영향을 받지 않음.
- 상속에 영향을 받지 않기 때문에 대부분의 경우 `rem` 을 많이 사용한다.
- Relative to font-size of the root element (default font size: 16px)
  - 1.5rem = 16px * 1.5

**viewport**

- (스크롤을 내리지 않은 상태에서) 웹 페이지를 방문한 유저에게 현재 보이는 웹 컨텐츠의 영역
- viewport를 기준으로한 상대적인 사이즈
- 주로 스마트폰이나 테블릿 디바이스의 화면을 일컫는 용어로 사용된다.
- vw, vh

<br>

## 색상 단위

1. 색상 키워드
   - 색상 키워드는 대소문자를 구분하지 않는 식별자로, red, blue, black처럼 특정 색을 나타냄
2. RGB 색상
   - 빨강, 초록, 파랑을 통해 특정 색을 표현
   - 16진수 표기법이나 함수형 표기법으로 사용
   - a는 alpha(투명도)가 추가된 것
3. HSL 색상
   - 색상, 채도, 명도를 통해 특정 색상을 표현
   - a는 alpha(투명도)가 추가된 것