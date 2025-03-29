# Form

## HTML ‘form’

- 지금까지 사용자로부터 **데이터를 제출받기 위해** 활용한 방법
- 비정상적 혹은 악의적인 요청을 필터링 할 수 없음.

⇒ 유효한 데이터인지에 대한 확인이 필요함.

- **유효성 검사** : 수집한 데이터가 정확하고 유효한지 확인하는 과정

## Django Form

- **사용자 입력 데이터를 수집**하고, **처리 및 유효성 검사**를 수행하기 위한 도구
    - 유효성 검사를 단순화하고 자동화할 수 있는 기능을 제공

### Form rendering options

- label, input 쌍을 특정 HTML태그로 감싸는 옵션

## Widgets

- HTML ‘`input`’ element의 표현을 담당
- 적용
    - Widget은 단순히 input 요소의 속성 및 출력되는 부분을 변경하는 것

---

# Django ModelForm

- Form : 사용자 입력 데이터를 DB에 저장하지 않을 대 (ex. 검색, 로그인)
- ModelForm : 사용자 입력 데이터를 **DB에 저장해야 할 때** (ex. 게시글 작성, 회원가입)

## ModelForm

- Model과 연결된 Form을 자동으로 생성해주는 기능을 제공
    - Form + Model
- ModelForm class 정의 : 기존 Form 클래스 수정
- “**사용자로부터 데이터를 수집하고 처리하기 위한 강력하고 유연한 도구**”
- HTML `form`의 생성, 데이터 유효성 검사 및 처리를 쉽게 할 수 있도록 도움.

## Meta class

- ModelForm의 정보를 작성하는 곳

### ‘`fields`’ 및 ‘`exclude`’ 속성

- `exclude` 속성을 사용하여 모델에서 포함하지 않을 필드를 지정할 수도 있음.

### Meta class 주의사항

- Django에서 `ModelForm`에 대한 추가 정보나 속성을 작성하는 클래스 구조를 `Meta` 클래스로 작성했을 뿐이며, 파이썬의 inner class와 같은 문법적인 관심으로 접근하지 말 것

### `is_valid()`

- 여러 **유효성 검사를 실행**하고, 데이터가 유효한지 여부를 `Boolean`으로 반환

### 공백 데이터가 유효하지 않은 이유와 에러메시지가 출력되는 과정

- 별도로 명시하지 않았지만, 모델 필드에는 **기본적으로 빈 값은 허용하지 않는 제약조건**이 설정되어 있음.
- 빈 값은 `is_valid()`에 의해 `False`로 평가되고 `form` 객체에는 그에 맞는 에러 메시지가 포함되어 다음 코드로 진행됨.

### `save()`

- 데이터베이스 객체를 만들고 저장하는 `ModelForm`의 인스턴스 메서드

### save() 메서드가 생성과 수정을 구분하는 법

- 키워드 인자 `instance` 여부를 통해 생성할지, 수정할지를 결정

---

# HTTP 요청 다루기

## View 함수 구조 변화

- new & create view 함수 간 공통점과 차이점
    - 공통점 : 데이터 생성을 구현하기 위함
    - 차이점 : new는 **GET** method 요청만을, create는 **POST** method 요청만을 처리

⇒ **HTTP request method 차이점을 활용해 동일한 목적을 가지는 2개의 view 함수를 하나로 구조화**

## new & create 함수 결합

- 새로운 create view 함수
    - new와 create view 함수의 **공통점과 차이점을 기반**으로 하나의 함수로 결합.
    - 두 함수의 유일한 차이점이었던 **request method에 따른 분기**
    - **POST**일 때는 과거 create 함수 구조였던 객체 생성 및 저장 로직
    - **POST**가 아닐 때는 과거 new 함수에서 진행했던 **`form`** 인스턴스 생성
    - context에 담기는 `form`은
        1. `is_valid()`를 통과하지 못해 에러 메시지를 담은 `form`이거나
        2. `else` 문을 통한 `form` 인스턴스
- 기존 new 관련 코드 수정
    - 사용하지 않게 된 new url 제거
    - new 관련 키워드를 create로 변경
    - render에서 new 템플릿을 create 템플릿으로 변경

### request method에 따른 요청의 변화

- **GET** : 게시글 생성 **페이지 줘**!
- **POST** : 게시글을 **생성해줘**!

## edit & update 함수 결합

- 새로운 update view 함수
    - 기존 edit과 update view 함수 결합
- 기존 edit 관련 코드 수정
    - 사용하지 않은 edit url 제거
    - edit 관련 키워드를 update로 변경

## ※ 참고

### ModelForm의 키워드 인자 구성

- ModelForm 키워드 인자 data와 instance 살펴보기
    - data는 첫 번째에 위치한 키워드 인자이기 때문에 생략 가능
    - instance는 9번째에 위치한 키워드 이기 때문에 생략할 수 없었음.
