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
  
3. 
4. 
