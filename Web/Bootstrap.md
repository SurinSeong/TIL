# Bootstrap

- CSS 프론트엔드 프레임워크 (Toolkit)
    - **미리 만들어진** 다양한 디자인 요소들을 제공하여 웹사이트를 빠르고 쉽게 개발할 수 있도록 함.

- **CDN** (Content Delivery Network) : **지리적 제약 없이** 빠르고 안전하게 콘텐츠를 전송할 수 있는 전송 기술
    - 서버와 사용자 사이의 **물리적 거리를 줄여** 콘텐츠 로딩에 소요되는 **시간을 최소화** (웹페이지 로드 속도 높임)
    - 지리적으로 사용자와 가까운 CDN 서버에 콘텐츠를 저장해서 사용자에게 전달
 
- 예시

```html

{property}{sides}-{size}
mt-5

```
- 클래스 규칙을 따라 클래스 명을 만든다.
- Bootstrap에서 클래스 이름으로 Spacing을 표현하는 방법
    - Property
        - m : margin
        - p : padding
    - Sides
        - t : top
        - b : bottom
        - s : left
        - e : right
        - y : top, bottom
        - x : left, right
        - blank : 4 sides
    - Size
        - 0 : 0 rem = 0px
        - 1 : 0.25 rem = 4px
        - 2 : 0.5 rem = 8px
        - 3 : 1 rem = 16px
        - 4 : 1.5 rem = 24px
        - 5 : 3 rem = 48
        - auto

※ Bootstrap에는 **특정한 규칙이 있는 클래스 이름**으로 스타일 및 레이아웃이 미리 작성되어 있다.

## Reset CSS

- 모든 HTML 요소 스타일을 일관된 기준으로 재설정하는 간결하고 압축된 규칙 세트
    - HTML Element, Table, List 등의 요소들에 일관성있게 스타일을 적용시키는 기본 단계

- 사용 배경
    - 모든 브라우저는 각자의 '**user agent stylesheet**'를 가지고 있음 (user agent stylesheet : 모든 문서에 기본 스타일을 제공하는 기본 스타일 시트)
        - 웹사이트를 보다 읽기 편하게 하기 위해
    - 문제는 이 설정이 브라우저마다 상이하다는 것
    - **모든 브라우저에서 웹사이트를 동일하게 보이게** 만들어야 하는 개발자에겐 매우 골치 아픈 일
        - **모두 똑같은 스타일 상태**로 만들고 스타일 **개발을 시작**하자!
     
### Normalize CSS

- Reset CSS 방법 중 대표적인 방법
- 웹 표준 기준으로 브라우저 중 하나가 불일치한다면 **차이가 있는 브라우저를 수정**하는 방법
    - 경우에 따라 IE 또는 EDGE 브라우저는 표준에 따라 수정할 수 없는 경우도 있는데, 이 경우 IE 또는 EDGE의 스타일을 나머지 브라우저에 적용시킴.
 
- Bootstrap에서의 Reset CSS
    - **bootstrap-reboot.css** => normalize.css를 자체적으로 커스텀해서 사용.
 
---

## 활용

### Typography

- 제목, 본문 텍스트, 목록 등의 표현 방식

1. Display headings
    - 기존 Heading보다 더 눈에 띄는 제목이 필요할 경우 (더 크고 약간 다른 스타일)

2. Inline text elements
    - HTML inline 요소에 대한 스타일
  
3. List
    - HTML list 요소에 대한 스타일
  
### Color

- Bootstrap Color system : Bootstrap이 지정하고 제공하는 색상 시스템
- Text, border, Background 및 다양한 요소에 사용하는 Bootstrap의 색상 키워드
- 사이트 제공 **규칙** 꼭 숙지하기!

### Conponent

- Bootstrap에서 제공하는 **UI 관련 요소**
    - 버튼, 네비게이션 바, 카드, 폼, 드롭다운 등

- 이점 : 일관된 디자인을 제공하여 웹사이트의 구성요소를 구축하는 데 유용하게 활용
 
- 대표 Component
    - Alerts ex) github
    - Badges
    - Buttons
    - **Cards** : 구성이 아주 많이 쓰인다.
        - 이미지 + 본문
        - [Card Docs](https://getbootstrap.com/docs/5.3/components/card/)
    - **Navbar** : 네비게이션 바도 아주아주 자주 쓰인다.
        - [Navbar Docs](https://getbootstrap.com/docs/5.3/components/navbar/)

---

## Semantic Web

- 웹 데이터를 **의미론적으로 구조화된 형태**로 표현하는 방식
    - "이 요소가 시각적으로 어떻게 보여질까?" --> "이 요소가 가진 목적과 역할은 무엇일까?"

### Semantic in HTML

- HTML 요소가 의미를 가진다는 것
- `<h1>Heading</h1>` : "**페이지 내 최상위 제목**"이라는 의미를 제공하는 요소 h1 => **브라우저에 의해 스타일이 지정**된다.

- HTML Sementic Element : 기본적인 모양과 기능 이외에 **의미**를 가지는 HTML 요소  
=> 검색엔진 및 개발자가 웹페이지 콘텐츠를 이해하기 쉽도록

- 대표적인 Semantic Element (전부 div와 똑같음)
    - header
    - nav
    - main
    - article
    - section
    - aside
    - footer

### Semantic in CSS

- CSS 방법론 : CSS를 효율적이고 유지 보수가 용이하게 작성하기 위한 일련의 가이드라인
- OOCSS (Object Oriented CSS) : **객체 지향적 접근법**을 적용하여 CSS를 구성하는 방법론

- OOCSS 기본 원칙 (**함수**처럼 **클래스** 만들기)
    1. 구조와 스킨을 분리
        - 구조와 스킨을 분리함으로써 재사용 가능성을 높임
        - 모든 버튼의 **공통 구조**를 정의 + **각각의 스킨**(배경색과 폰트 색상)을 정의

    2. 컨테이너와 콘텐츠를 분리
        - 객체에 직접 적용하는 대신 **객체를 둘러싸는 컨테이너에 스타일을 적용**
        - 스타일을 정의할 때, 위치에 의존적인 스타일을 사용하지 않도록 함
        - 콘텐츠를 다른 컨테이너로 이동시키거나 재배치할 때, 스타일이 깨지는 것을 방지

---

### Bootstrap을 사용하는 이유

- 가장 많이 사용되는 CSS 프레임워크
- 사전에 디자인된 다양한 컴포넌트 및 기능
    - 빠른 개발과 유지보수
- 손쉬운 반응형 웹 디자인 구현
- 커스터마이징이 용이
- 크로스 브라우징 지원
    - 모든 주요 브라우저에서 작동하도록 설계되어 있음
 
### 의미론적 마크업이 필요한 이유

- 검색엔진 최적화 (SEO)
    - 검색 엔진이 해당 웹사이트를 분석하기 쉽게 만들어 검색 순위에 영향을 줌.

- 웹 접근성 (Web Accessibility)
    - 웹사이트, 도구, 기술이 고령자나 장애를 가진 사용자들이 사용할 수 있도록 설계 및 개발하는 것
