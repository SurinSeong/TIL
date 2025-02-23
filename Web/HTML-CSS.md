# HTML & CSS

## 웹

- World Wide Web : 인터넷으로 연결된 컴퓨터들이 정보를 공유하는 거대한 정보 공간
- Web : Website, Web application 등 (웹으로 만든 프로그램들)을 통해 사용자들이 정보를 검색하고 상호작용하는 기술의 총칭
- Web site : 인터넷에서 여러 개의 Web page가 모인 것, 사용자들에게 정보나 서비스를 제공하는 공간
- Web page : HTML, CSS 등의 웹 기술을 이용하여 만들어진, "Web site"를 구성하는 하나의 요소
    - 구성요소
        - HTML : 구조
        - CSS : 스타일
        - Javascript : 행동  
    => 위의 세 가지의 기술이 서로 상호보완적으로 작용하며 Web page를 구성하게 된다.

## 웹 구조화

- HTML : HyperText Markup Language  
  웹 페이지의 **의미**와 **구조**를 정의하는 언어

- Hypertext : 웹페이지를 다른 페이지로 연결하는 링크  
  **참조**를 통해 사용자가 한 문서에서 다른 문서로 즉시 접근할 수 있는 텍스트

    - 특징 : 비선형성 / 상호연결성 / 사용자 주도적 탐색
 
- Markup Language : 태그 등을 이용하여 문서나 데이터의 구조를 명시하는 언어  
  ex) HTML, Markdown

### HTML 구조

- `<!DOCTYPE html>` : 해당 문서가 html로 문서라는 것을 나타냄.
- `<html></html>` : 전체 페이지의 콘텐프를 포함.
- `<title></title>` : 브라우저 탭 및 즐겨찾기 시 표시되는 제목으로 사용.
- `<head></head>` : HTML 문서에 관련된 설명, 설정 등 **컴퓨터가 식별**하는 **메타데이터**를 작성, **사용자에게 보이지 않음**.
    - 메타 데이터 : 데이터에 대한 데이터
- `<body></body>` : HTML 문서의 내용을 나타냄. 페이지에 표시되는 모든 콘텐츠를 작성. **한 문서에 하나의 body 요소만 존재**.

- HTML Element (요소)
    - 하나의 요소는 **여는 태그**와 **닫는 태그** 그리고 그 안의 내용(콘텐츠)으로 구성됨.
    - 닫는 태그는 태그 이름 앞에 슬래시가 포함됨.
        - 닫는 태그가 없는 태그도 존재함. (콘텐츠가 없음.)
     
- HTML Attributes (속성)
    - 사용자가 원하는 기준에 맞도록 **요소를 설정**하거나 다양한 방식으로 **요소의 동작을 조절**하기 위한 값
    - 목적
        - 나타내고 싶지 않지만 (사용자에게 보여지지는 않음.) 추가적인 기능, 내용을 담고 싶을 때 사용
        - **CSS**에서 스타일 적용을 위해 해당 요소를 **선택하기 위한** 값으로 활용됨.
    
    - 작성 규칙
        - 속성은 요소 이름과 속성 사이에 공백이 있어야 함.
        - 하나 이상의 속성들이 있는 경우, 속성 사이에 공백으로 구분.
        - 속성 값은 열고 닫는 따옴표로 감싸야 함.
     
### Text Structure

- Heading & Paragraphs
    - h1~6, p
    - 되도록 하나의 문서에서는 h1은 하나만 존재하는 것이 좋다.

- Lists
    - ol, ul, li

- Emphasis & Importance
    - em, strong
 
---

## 웹 스타일링

### CSS

- CSS : 웹페이지의 **디자인**과 **레이아웃**(배치)을 구성하는 언어

<details>
    <summary>CSS 구문</summary>

```
h1 {
    color: red;
    font-size: 30px;
}
```

- `h1` : 선택자 (Selector)
- `color: red;` : 선언 (Declaration)
- `font-size` : 속성 (Property)
- `30px` : 값 (Value)

</details>

- 적용방법

1. 인라인(Inline) 스타일

- HTML 요소 안에 style 속성 값으로 작성

2. **내부**(Internal) 스타일 시트

- head 태그 안에 style 태그에 작성
- 주로 내부 방식을 사용한다.

3. 외부(External) 스타일 시트

- **별도 CSS 파일 생성** 후 HTML link 태그를 사용해 불러오기
- 외부의 파일을 생성해서 불러오는 방식으로 사용한다.

### CSS 선택자 (Selectors)

- HTML 요소를 선택하여 **스타일을 적용**할 수 있도록 하는 선택자

<details>
    <summary>종류</summary>

- 기본 선택자
    - 전체(*) 선택자 : HTML 모든 요소를 선택
    - 요소(tag) 선택자 : 지정한 모든 태그를 선택
    - 클래스(class) 선택자 ('.') : 주어진 클래스 속성을 가진 모든 요소를 선택 (**재사용**)
    - 아이디(id) 선택자 ('#') : 주어진 아이디 속성을 가진 요소 선택. 문서에는 주어진 아이디를 가진 요소가 **하나만** 있어야 한다.
    - 속성(attr) 선택자

- 결합자 (태그 안에 상하관계가 존재함.)
    - 자손 결합자 (' ') : 첫 번째 요소의 자손 요소들 선택
    - 자식 결합자 ('>') : 첫 번째 요소의 직계 자식(한 단계 아래)만 선택

</details>

### 명시도 (Specificity)

- 결과적으로 요소에 적용할 CSS 선언을 결정하기 위한 알고리즘
- CSS Selector에 가중치를 계산하여 어떤 스타일을 적용할지 결정
    - 동일한 요소를 가리키는 2개 이상의 CSS 규칙이 있는 경우, 가장 높은 명시도를 가진 Selector가 승리하여 스타일이 적용됨.
 
- Cascade : 한 요소에 동일한 가중치를 가진 선택자가 적용될 때 CSS에서 **마지막에 나오는 선언**이 사용된다.

<details>
    <summary>명시도가 높은 순</summary>

1. Importance
2. Inline 스타일
3. 선택자
    - id 선택자 > class 선택자 > 요소 선택자 (좁은 범위 선택 -> 명시도 높음.)
4. 소스코드 선언 순서

</details>

### 상속

- 기본적으로 CSS 상속을 통해 부모 요소의 속성을 자식에게 상속해 **재사용성**을 높임.

<details>
    <summary>분류</summary>

- 상속되는 속성
    - Text 관련 요소 : font, color, text-align, opacity, visibility
- 상속되지 않는 속성
    - Box model 관련 요소 : width, height, border, box-sizing
    - position 관련 요소 : position, top/right/bottom/left, z-index
 
</details>

## CSS Box Model

- 웹 페이지의 모든 HTML 요소를 감싸는 **사각형 상자** 모델

<details>
    <summary>박스 타입</summary>

1. Block box : 오른쪽
2. Inline box : 아래

=> 박스 타입에 따라 페이지에서의 배치 흐름 및 다른 박스와 관련하여 박스가 동작하는 방식이 달라짐.

</details>

<details>
    <summary>박스 표시 타입</summary>

1. Outer display type : 박스가 문서 흐름에서 어떻게 동작할지를 결정

- Block
    - 항상 새로운 행으로 나뉨
    - width와 height 속성 사용 가능
    - padding, margin, border로 인해 다른 요소를 상자로부터 밀어냄
    - width 속성을 지정하지 않으면 박스는 inline 방향으로 사용 가능한 공간을 모두 차지 함.
        - 상위 컨테이너 너비 100%로 채우는 것
    - 대표적인 block 타입 태그 : h1~6, p, div

- Inline
    - 새로운 행으로 넘어가지 않음
    - width와 height 속성을 사용할 수 없음.
    - 수직 방향
        - padding, margin, border가 적용되지만, 다른 요소를 밀어낼 수는 없음.
    - 수평 방향
        - padding, margin, border가 적용되어 다른 요소를 밀어낼 수 있음.
    - 대표적인 inline 타입 태그 : a, img, span, strong, em
  
2. Inner display type : 박스 내부의 요소들이 어떻게 배치될지를 결

=> 박스 타입에 따라 페이지에서의 배치 흐름 및 다른 박스와 관련하여 박스가 동작하는 방식이 달라짐.

</details>

