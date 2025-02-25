# CSS Layout

## CSS Box Model

- 웹페이지의 모든 HTML 요소를 감싸는 **사각형 상자** 모델
    - 내용(content), 안쪽 여백(padding), 테두리(border), 외부 간격(margin)으로 구성되어 요소의 크기와 배치를 결정

<details>
    <summary>Box 구성 요소</summary>

- Margin : 이 박스와 다른 요소 사이의 공백, **가장 바깥쪽** 영역. `margin` 관련 속성을 사용하여 크기 조정
- Border : 콘텐츠와 패딩을 **감싸는** 테두리 영역. `border` 관련 속성을 사용하여 크기 조정
- Content : **실제 콘텐츠**가 표시되는 영역. `width` 및 `height` 속성을 사용하여 크기 조정.
- Padding : 콘텐츠 주위에 위치하는 **공백**. `padding` 관련 속성을 사용하여 크기 조정.

</details>

- shorthand 속성
    - `border` : border-width, border-style, border-color를 한번에 설정하기 위한 속성
    - `margin` & `padding` : 4방향의 속성을 각각 지정하지 않고 한번에 지정할 수 있는 속성
    - 
