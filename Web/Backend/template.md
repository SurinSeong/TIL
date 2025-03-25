# Django Template System

- 데이터 표현을 제어하면서, **표현**과 관련된 부분을 담당

## Django Template Language (DTL)

- Template에서 조건, 반복, 변수 등의 프로그래밍적 기능을 제공하는 시스템

### DTL Syntax

1. Variable
    - `render` 함수의 세 번째 인자로 **딕셔너리 데이터**를 사용한다.
    - 딕셔너리 **key에 해당하는 문자열**이 template에서 **사용가능한 변수명**이 된다.
    - **dot(.)을 사용해 변수 속성에 접근**할 수 있다.
2. Filters
    - **표시할 변수를 수정**할 때 사용 (변수 | 필터)
    - **chained**이 가능하고 일부 필터는 인자를 받기도 한다.
    - 약 60개의 **built-in template filters**를 제공한다.
3. Tags
    - **반복 또는 논리**를 수행하여 제어 흐름을 만든다.
    - 일부 태그는 **시작과 종료 태그**가 필요하다.
    - 약 24개의 built-in template tags를 제공한다.
4. Comments
    - DTL에서의 **주석**

## 템플릿 상속

### 기본 템플릿 구조의 한계

- 만약 모든 템플릿에 bootstrap을 적용하려면?
    - 모든 템플릿에 bootstrap CDN을 작성해야할까?

### 템플릿 상속

- 페이지의 **공통 요소를 포함**하고, 하위 템플릿이 **재정의할 수 있는 공간을 정의**하는 **기본 skeleton 템플릿**을 작성하여 **상속 구조**를 구축한다.

- 상속 구조 만들기
    - body 태그 안에 block 태그를 넣어준다.
        
        ```html
        {% block content %}
        {% endblock content %}
        ```
        

## 상속 관련 DTL 태그

- `extends` tag : 자식(하위) 템플릿이 부모 템플릿을 확장한다는 것을 알린다.
    - 반드시, 자식 템플릿 최상단에 작성되어야 한다. (하나만 사용가능)
- `block` tag : 하위 템플릿에서 재정의할 수 있는 블록을 정의 (상위 템플릿에 작성하며 하위 템플릿이 작성할 수 있는 공간을 지정하는 것)

## 요청과 응답

### HTML Form

- 데이터를 보내고 가져오기
    - HTML `form` element를 통해 사용자와 애플리케이션 간의 상호작용 이해
        - `form` - `input` 관계 중요!

- `form` element
    - 사용자로부터 할당된 데이터를 서버로 전송
        - 웹에서 사용자 정보를 입력하는 여러 방식

## HTML form 핵심 속성

### action & method

- 데이터를 어디(action)로 어떤 방식(method)으로 요청할지
- action
    - 입력데이터가 전송될 URL을 지정 (목적지)
    - 만약 이 속성을 지정하지 않으면 데이터는 현재 form이 있는 페이지의 URL로 보내짐
- method
    - 데이터를 어떤 방식으로 보낼 것인지 정의
    - 데이터의 HTTP request methods (GET, POST)를 지정

### input element

- 사용자의 데이터를 입력받을 수 있는 요소 (**type 속성 값에 따라** 다양한 유형의 입력 데이터를 받음)
    - 핵심 속성 - `name`

- `name` attribute
    - **input**의 핵심 속성
    - 사용자가 입력한 데이터에 붙이는 이름 (**key**)
    - 데이터를 제출했을 때, 서버는 **name 속성에 설정된 값을 통해서만** 사용자가 입력한 데이터에 접급할 수 있음.

### Query String Parameters

- 사용자의 입력데이터를 URL 주소에 파라미터를 통해 서버로 보내는 방법
- 문자열은 ‘&’로 연결된 key=value쌍으로 구성되며, 기본 URL과는 물음표로 구분된다.

## Django URLs

### URL dispatcher

- URL 패턴을 정의하고 해당 패턴이 일치하는 요청을 처리할 view 함수를 연결

### Variable routing

- URL 일부에 변수를 포함시킨다.
    - 변수는 view 함수의 인자로 전달할 수 있음.

## App과 URL

### App URL mapping

- 각 앱에 URL 정의
    - 프로젝트와 각 앱이 URL을 나누어 관리를 편하게 하기 위함.

### Naming URL patterns

- url이 복잡해졌을 때, name을 설정해서 간단하게 가져올 수 있다.
