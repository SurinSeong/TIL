# Django Model & ORM

## Django Model

- **DB의 테이블을 정의**하고 **데이터를 조작**할 수 있는 기능들을 제공
    - 테이블 구조를 설계하는 **청사진**

### model 클래스 살펴보기
 
- 작성한 모델 클래스는 최종적으로 DB에 다음과 같은 테이블 구조를 만든다.
- django.db.models 모듈의 Model이라는 부모 클래스를 상속받음.
- Model은 model에 관련된 모든 콛드가 이미 작성되어 있는 클래스이다.
- 구성
    1. 클래스 변수명 : 테이블의 각 **필드(열) 이름**
    2. model Field 클래스 : 테이블 필드의 **데이터 타입**
    3. model Field 클래스의 키워드 인자 (필드 옵션) : 테이블 필드의 **제약조건** 관련 설정
        - 제약조건 : 데이터가 올바르게 저장되고 관리되도록 하기 위한 규칙 
- 상속의 좋은점 : 파이썬 문법에 맞게 데이터베이스를 관리할 수 있다.

## Migrations

- 파이썬으로 작성한 클래스를 실제 데이터베이스에 반영하는 방법
- model 클래스의 **변경사항** (필드 생성, 수정, 삭제 등)을 DB에 **최종 반영**하는 방식

- Migrations 과정

1.  model class (설계도 초안) 생성
    - views.py에 사용할 클래스를 생성한다.

2.  migration 파일 (최종 설계도)
    - 데이터 베이스에 반영된다.

3.  db.sqlite3

- Migrations 핵심 명령어 2가지
- `$python manage.py makemigrations` : model class를 기반으로 **최종 설계도** (migration) 작성
- `$python manage.py migrate` : 최종 설계도를 **DB에 전달하여 반영**
    - sqlite3 생성된다.

- Migrate 후 DB 내에 생성된 테이블 확인
    - Article 모델 클래스로 만들어진 articles_article 테이블

- 이미 생성된 테이블에 필드를 추가해야 한다면?? >> **클래스에 테이블 추가**한다.
    - 이때, 데이터베이스의 값은 비어있으면 안된다.
    - 따라서, 필드를 추가해준다면, 이미 기존 테이블이 존재하기 때문에 필드를 추가할 때, 필드의 기본 값 설정이 필요하다.
        - 1) 현재 대화를 유지하며 직접 기본 값을 입력하는 방법 = 실행과정을 종료하지 않고 다음 번에 다시 물어본다.
         
            - 아무것도 입력하지 않고 enter 두번 누르면 django가 제안하는 기본 값으로 설정된다.
            - migrations 과정이 죵료된 후, 2번째 migration 파일 (설계도) 이 생성된 것을 확인할 수 있다.
          
        - 2) 현재 대화에서 나간 후, models.py에 기본값 관련 설정을 하는 방법
            
            - default 값에 대한 제약사항을 넣을 수 있다.
         
※ Model class에 **변경사항**이 생겼다면, 반드시 **새로운 설계도를 생성**하고 이를 **DB에 반영**해야 한다.

### 모델 필드

- Model Field : DB 테이블의 **필드**(열)을 정의하며, 해당 필드에 저장되는 **데이터 타입**과 **제약조건**을 정의
    - `CharField()` : **길이의 제한이 있는** 문자열을 넣을 때 사용. (필드의 최대 길이를 결정하는 **max_length는 필수 인자**이다.)
    - `TextField()` : 글자의 수가 많을 때 사용
    - `DateTimeField()` : 날짜와 시간을 넣을 때 사용
 
### Admin site


# ORM (Object Relational Mapping)

- **객체 지향 프로그래밍 언어**를 사용하여 **호환되지 않는 유형의 시스템 간에 데이터를 변환**하는 기술

## 역할

- 사용하는 언어가 다르기 때문에 소통할 수 없음.
    - Django에 내장된 ORM이 중간에서 이를 해석
    

## QuerySet API

- ORM 에서 **데이터를 검색, 필터링, 정렬 및 그룹화** 하는 것에 사용하는 도구
    - **API를 사용**하여 SQL이 아닌 **Python 코드**로 데이터를 처리

- QuerySet API 구문
    
    ```python
    # Model class | Manager | QuerySet API
    Article.objects.all()
    ```
    
    1. 어떠한 객체가 가지고 있는 속성 개체 메서드를 호출하면 ORM 동작
    2. 전체 API 문장을 읽고 내용 파악 후 데이터베이스에 요청을 보낸다.
    3. 데이터베이스에서 내용에 대한 응답을 ORM에게 넘겨주고
    4. ORM은 응답을 python에서 사용할 수 있는 타입으로 변환해서 전달한다.

- Query
    - DB에 특정한 데이터를 보여 달라는 **요청**
    - “쿼리문을 작성한다.”
        - 원하는 데이터를 얻기 위해 DB에 요청을 보낼 코드를 작성한다.
    - **파이썬으로 작성한 코드가 ORM에 의해 SQL로 변환되어 DB에 전달되며, DB의 응답 데이터 ORM이 QuerySet이라는 자료 형태로 변환하여 전달**한다.
- QuerySet
    - DB에게서 전달받은 객체 목록 (**데이터 모음**)
        - 순회가 가능한 데이터로써 1개 이상의 데이터를 불러와 사용 가능하다
    - **Django ORM을 통해 만들어진 자료형** (= python의 리스트처럼 사용할 수 있음.)
        - for문 사용 가능
    - 단, DB가 **단일한 객체를 반환**할 때는 QuerySet이 아닌 **모델(Class)의 인스턴스로 반환**된다.

### QuerySet API는 python의 모델 클래스와 인스턴스를 활용해 DB에 데이터를 저장, 조회, 수정, 삭제하는 것!

# Serialization (직렬화)

- 여러 시스템에서 활용하기 위해 데이터 구조나 객체 상태를 나중에 **재구성할 수 있는 포맷으로 변환**하는 과정
- **어떠한 언어나 환경**에서도 나중에 **다시 쉽게 사용할 수 있는 포맷**으로 변환하는 과정
- 예시)
    - DB에서 가지고 온 객체 정보 >> 직렬화된 데이터 >> JsonResponse 가능
    - Serializer Class!
 
## Serializer

- Serialization을 진행하여 Serialized data를 반환해주는 클래스
- ModelSerializer : Django 모델과 연괄된 Serializer 클래스
    - 일반 Serializer와 달리 사용자 입력 데이터를 받아 **자동으로 모델 필드에 맞추어** Serialization을 진행
    - 

