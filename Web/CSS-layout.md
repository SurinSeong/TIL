# CSS Layout

- 각 요소의 **위치**와 **크기**를 조정하여 웹페이지의 디자인을 결정하는 것.

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
    - `margin` & `padding` : 4방향(상우하좌)의 속성을 각각 지정하지 않고 한번에 지정할 수 있는 속성

- box-sizing 속성
    - The standard CSS box model : 표준 상자 모델에서 width와 height 속성 값을 설정하면 이 값은 **content box의 크기**를 조정하게 됨.
    - The alternative CSS box model : 대체 상자 모델에서 모든 width와 height는 실제 상자의 너비. 실제 박스 크기를 정하기 위해 테두리와 패딩을 조정할 필요 없음.

### 기타 display 속성

- 'inline block' : inline과 block 요소 사이의 중간 지점을 제공하는 display값
    - width와 height 속성 사용 가능
    - padding. margin, border로 인해 다른 요소가 상자에서 밀려남
    - 새로운 행으로 넘어가지 않음.  
    => **요소가 줄바꿈되는 것을 원하지 않으면서, 너비와 높이를 적용하고 싶은 경우에 사용**

- `none` : 요소를 화면에 표시하지 않고, 공간조차 부여되지 않음.

---

## CSS Position

- 요소를 Normal flow에서 제거하여 **다른 위치로 배치**하는 것.
    - 다른 요소 위에 올리기, 화면의 특정 위치에 고정시키기
 
### 유형
1. static
2. relative
3. absolute
4. fixed
5. sticky
    - 평소에는 relative, 어느 순간 (스크롤의 위치가 임계점에 도달하는 순간) fixed
  

### z-index

- 요소의 쌓임 순서 (stack order)를 정의하는 속성
- 정수 값을 사용해 Z축 순서를 지정
- 값이 클수록 요소가 위에 쌓이게 됨 ==> 항상 위에 있도록 하고 싶을 경우 1000으로 두는 경우도 있음. 
- static이 아닌 요소에만 적용됨

- 특징
    - 기본값 : auto
    - 부모 요소의 z-index값에 영향을 받음
    - 같은 부모 내에서만 z-index값을 비교
    - 부모의 z-index가 낮으면 자식의 z-index가 아무리 높아도 부모보다 위로 올라갈 수 없음.
    - z-index값이 같으면 HTML 문서 순서대로 쌓임.
 
※ Position의 목적 : 전체 페이지에 대한 레이아웃을 구성하는 것보다는 ***페이지 특정 항목의 위치를 조정**하는 것

---

## CSS Flexbox

- 요소를 **행과 열** 형태로 배치하는 **1차원** 레이아웃 방식
    - **공간 배열 & 정렬**

### 구성 요소

- Main axis (주 축)
    - flex item들이 배치되는 기본 축
    - main start에서 시작하여 main end 방향으로 배치 (기본 값)

- Cross axis (교차 축)
    - main axis에 수직인 축
    - cross start에서 시작하여 cross end 방향으로 배치 (기본 값)

- Flex Container
    - `display: flex;` or `display: inline-flex;`가 설정된 부모 요소
    - 이 컨테이너의 1차 자식 요소들이 Flex Item이 됨.
    - flexbox 속성 값들을 사용하여 자식 요소 flex item들을 배치하는 주체

- Flex item
    - Flex Container 내부에 레이아웃 되는 항목
 
### 속성

1. Flex Container 지정
- flex item은 기본적으로 행으로 나열
- flex item은 주 축의 시작 선에서 시작
- flex item은 교차 축의 크기를 채우기 위해 늘어

2. flex-direction (배치)
- flex item이 나열되는 방향을 지정
- column으로 지정할 경우 주 축이 변경됨
- '-reverse'로 지정하면 flex item 배치의 시작 선과 끝 선이 서로 바뀜

3. flex-wrap (배치) : flex item 목록이 flex container의 한 행에 들어가지 않을 경우, 다른 행에 배치할지 여부 설정
4. justify(main axis)-content (분배) : **주 축**을 따라 flex item과 주위에 공간을 분배
- '-item', '-self' 속성이 없는 이유 : margin auto를 통해 정렬 및 배치가 가능

5. align-content (분배) : 교차 축을 따라 flex item과 주위에 공간을 분배
    - flex-wrap이 wrap 또는 wrap-reverse로 설정된 여러 행에만 적용됨.
    - 한 줄짜리 행에는 효과 없음 (flex-wrap이 nowrap으로 설정된 경우)

6. align-items (정렬) : 교차 축을 따라 flex item 행을 정렬
7. align-self (정렬) : 교차 축을 따라 개별 flex item을 정렬
8. flex-grow : 남는 행 여백을 비율에 따라 각 flex item에 분배
    - 아이템이 컨테이너 내에서 확장하는 비율을 지정
    - 남는 영역을 n등분해서 나눠주는!
9. flex-basis : flex item의 초기 크기 값을 지정
    - flex-basis와 width 값을 동시에 적용한 경우 **flex-basis**가 우선이다.

### flex wrap 응용

- 반응형 레이아웃 : 다양한 디바이스와 화면 크기에 **자동으로 적응**하여 콘텐츠를 최적으로 표시하는 웹 레이아웃 방식

---

## 참고

- 마진 상쇄 : 일관된 레이아웃 때문에
