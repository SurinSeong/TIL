# ORM

## QuerySet API

- ORM에서 데이터를 검색, 필터링, 정렬 및 그룹화 하는 것에 사용하는 도구
    - API를 사용하여 SQL이 아닌 Python 코드로 데이터를 처리한다.

### 구문

Article.objects.all()

⇒ 전체 게시글 조회 요청

이 문장이 SQL로 변환해서 DB에 전달하고, DB의 응답을 다시 ORM이 파이썬으로 변환해서 응답을 보여줄 수 있도록 한다.

all() → ‘QuerySet’

### Query

- 데이터베이스에 특정한 데이터를 보여달라는 요청
- “쿼리문을 작성한다.”
    - 원하는 데이터를 얻기 위해 데이터베이스에 요청을 보낼 코드를 작성한다.
- 파이썬으로 작성한 코드가 ORM에 의해 SQL로 변환되어 DB에 전달되며, DB의 응답 데이터를 ORM이 QuerySet이라는 자료형태로 변환하여 우리에게 전달

### QuerySet

- DB에게 전달받은 객체 목록 (데이터 모음)
    - 순회가 가능한 데이터로써 1개 이상의 데이터를 불러와 사용할 수 있음.
- Django ORM을 통해 만들어진 자료형
    - [Queryset] : 리스트 처럼 사용가능함.
- 단, DB가 단일한 객체를 반환할 때는 QuerySet이 아닌 **모델의 인스턴스**로 반환됨.

**QuerySet API는 python의 모델 클래스와 인스턴스를 활용해 DB에 데이터를 저장, 조회, 수정, 삭제 (CRUD)하는 것**

- django-extensions 문서 확인하기
    
    https://django-extensions.readthedocs.io/en/latest/
    
- shell_plus로 이용하기
`$ python [manage.p](http://manage.py)y shell_plus`
    - from articles.models import Article
        
        ⇒ 나의 model 클래스를 import 해준다.
        

데이터 생성 첫 번째 방법

1. 특정 테이블에 새로운 행을 추가하여 데이터를 추가한다.
2. save를 호출하고 확인하면 저장

⇒ 인스턴스 article을 활용해 인스턴스 변수 활용하기

데이터 생성 두 번째 방법

- save 메서드를 호출해야 비로소 DB에 데이터가 저장된다.
- 테이블에 한 행이 쓰여진다.

데이터 생성 세 번째 방법

- QuerySet API 중 create() 메서드 활용

Django >> id는 pk(prrmary key)로 사용한다.

## QuerySet API 메서드

### 조회 (Create)

- Return new QuerySets → 변수에 담을 수 있음.
    - all()
    - filter()
- Do not Return QuerySets
    - get() : 주어진 매개변수와 일치하는 객체를 **하나만!** 반환
        - 객체를 찾을 수 없으면 DoesNotExist 예외 발생
        - 둘 이상의 객체를 찾으면 MultipleObjectsReturned 예외 발생
        
        ⇒ **primary key와 같이 고유성을 보장하는 조회**에서 사용해야 한다.
        

### 수정 (Update)

1. **조회** 부터 할 수 있어야 수정이 가능하다. **(Point!!)**
2. 조회했다면 변수에 재할당해주고 저장을 해주면된다.
    
    save 하지 않으면 django에서만 변한 것 >> DB에 변경사항을 전달하지 않음!

---
# ORM with View

## Create

- Create 로직을 구현하기 위해 필요한 view 함수의 개수는? 2개!
    - new : 사용자 입력 데이터를 받을 페이지를 렌더링
    - create : 사용자가 입력한 요청 데이터를 받아 DB에 저장.

## HTTP request methods

### HTTP

- 네트워크 상에서 데이터(리소스)를 주고 받기 위한 약속

### HTTP request methods

- 데이터에 대해 수행을 원하는 작업(행동)을 나타내는 것
    - 서버에게 원하는 작업의 종류를 알려주는 역할
- 클라이언트가 웹 서버에 특정 동작을 요청하기 위해 사용하는 표준 명령어
- 대표 메서드
    - GET, POST

### GET Method

- 서버로부터 데이터를 요청하고 받아오는데(**조회**) 사용
- 특징
    1. 데이터 전송
        - URL의 쿼리 문자열 (Query String) 을 통해 데이터를 전송
    2. 데이터 제한
        - URL 길이에 제한이 있어 대량의 데이터 전송에는 적합하지 않음.
    3. 브라우저 히스토리
        - 요청 URL이 브라우저 히스토리에 남음
    4. 캐싱
        - 브라우저는 GET 요청의 응답을 로컬에 저장할 수 있음.
        - 동일한 URL로 다시 요청할 때, 서버에 접속하지 않고 저장된 결과를 사용
        - 페이지 로딩 시간을 크게 단축
- 사용 예시
    - 검색 쿼리 전송
    - 웹페이지 요청
    - API 에서 데이터 조회

### POST method

- 서버에 데이터를 제출하여 리소스를 변경(**생성, 수정, 삭제**)하는 것에 사용
- 특징
    1. 데이터 전송
        - HTTP Body를 통해 데이터 전송
    2. 데이터 제한
        - GET에 비해 더 많은 양의 데이터를 전송할 수 있음.
    3. 브라우저 히스토리
        - POST 요청은 브라우저 히스토리에 남지 않는다.
    4. 캐싱
        - POST 요청은 기본적으로 캐시할 수 없음.
        - POST 요청이 일반적으로 서버의 상태를 변경하는 작업을 수행하기 때문
- 사용 예시
    - 로그인 정보 제출
    - 파일 업로드
    - 새 데이터 생성 (예: 새 게시글 작성)
    - API에서 데이터 변경 요청

## HTTP response status code

- 서버가 클라이언트의 요청에 대한 처리 결과를 나타내는 3자리 숫자

### 역할

- 클라이언트에게 요청 처리 결과를 명확히 전달
- 문제 발생 시 디버깅에 도움
- 웹 애플리케이션의 동작을 제어하는 것에 사용

### 403 Forbidden

- 서버에 요청이 전달되었지만, 권한 때문에 거절되었다는 것을 의미
    - CSRF token 누락

### CSRF (Cross-site-Requesst-Forgery)

- 사이트 간 요청 위조
    - 사용자가 자신의 의지와 무관하게 공격자가 의도한 행동을 하여 특정 웹페이지를 보안에 취약하게 하거나 수정, 삭제 등의 작업을 하게 만드는 공격 방법
- 적용
    - DTL의 csrf_token 태그를 사용해 손쉽게 사용자에게 토큰 값을 부여
    - 요청 시 토큰 값도 함께 서버로 전송될 수 있도록 하는 것
        - Django 서버는 해당 요청이 DB에 데이터 하나 생성하는 (DB에 영향을 주는) 요청에 대해 **Django가 직접 제공한 페이지에서 데이터를 작성하고 있는 것인지**에 대한 확인 수단이 필요한 것
        - 겉모습이 똑같은 위조 사이트나 정상적이지 않은 요청에 대한 방어수단
- 왜 POST 일 때만 Token을 확인할까?
    - POST는 단순 조회를 위한 GET과 달리 특정 리소스에 변경을 요구하는 의미와 기술적인 부분을 가지고 있다.
    - DB에 조작을 가하는 요청은 반드시 인증 수단이 필요하다.
        - 데이터 베이스에 대한 **변경사항을 만드는 요청**이기 때문에 토큰을 사용해 **최소한의 신원 확인**을 하는 것이다.
- 게시글 작성 결과
    - 게시글 생성 후 **URL에 Query String 형태로 보냈던 데이터가 표기되지 않음.**

### Redirect

- 서버는 데이터 저장 후 페이지를 응답하는 것이 아닌 **사용자를 적절한 기존 페이지로 보내야 한다**.
    - 사용자를 보낸다. ⇒ 사용자가 **GET 요청을 한번 더 보내도록** 해야 한다.
    - 실제로 서버가 클라이언트를 직접 다른 페이지로 보내는 것이 아닌 **클라이언트가 GET 요청을 한번 더 보내도록 응답하는 것**
- 클라이언트가 **인자에 작성된 주소로 다시 요청을 보내도록** 하는 함수
- 동작원리
    1. redirect 응답을 받은 클라이언트는 detail url로 다시 요청을 보내게 된다.
    2. 결과적으로 detail view 함수가 호출되어 detail view 함수의 반환결과인 detail 페이지를 응답 받게 되는 것
    
    ⇒ 결국 사용자는 게시글 작성 후 작성된 게시글의 detail 페이지로 이동하는 것으로 느끼게 된다.
    

### Update

- 로직 구현을 위해 필요한 view 함수 개수는?
    - edit : 사용자 입력 데이터를 받을 페이지 렌더링
    - update : 사용자가 입력한 데이터를 받아 DB에 저장

## 참고

- GET 요청이 필요한 경우
    1. 캐싱 및 성능
        - GET 요청은 캐시 될 수 있고, 이전에 요청한 정보를 새로 요청하지 않고, 사용할 수 있음.
        - 특히, 동일한 검색 결과를 여러 번 요청하는 경우, GET 요청은 캐시를 활용하여 더 빠르게 응답할 수 있음.
    2. 가시성 및 공유
        - GET 요청은 URL에 데이터가 노출되어 있기 때문에 사용자가 해당 URL을 북마크하거나 다른 사람과 공유하기 용이
    3. RESTful API 설계
        - HTTP 메서드의 의미에 따라 동작하도록 디자인된 API의 일관성을 유지할 수 있음.
- **HTTP request methods를 활용한 효율적인 URL 구성**
    - **동일한 URL 한 개로 method에 따라 서버에 요구하는 행동을 다르게 요구!**

## 캐시 (cache)

- 데이터나 정보를 임시로 저장해두는 메모리나 디스크 공간
- 이전에 접근한 데이터를 빠르게 검색하고 접근할 수 있도록 함.
