# Model

## Model class

- Django Model : **DB의 테이블을 정의**하고 **데이터를 조작(생성(Create), 조회(Read), 수정(Update), 삭제(Delete))**할 수 있는 기능들을 제공
    - 테이블 구조를 설계하는 청사진
    - DB에게 계속해서 무언가를 전달하는 역할
- Model class 살펴보기
    - 작성한 모델 클래스는 최종적으로 **DB에 다음과 같은 테이블 구조를 만든다.**
    
    | id | title | content |
    | --- | --- | --- |
    | .. | .. | .. |
    | .. | .. | .. |
    
    - id 필드는 자동 생성
    - `django.db.models` 모듈의 `Model`이라는 부모 클래스를 상속받음
        - Model은 model에 관련된 모든 코드가 이미 작성되어 있는 클래스
    - 개발자는 **가장 중요한 테이블 구조를 어떻게 설계할지**에 대한 코드만 작성하도록 하기 위한 것 (상속을 활용한 프레임워크의 기능 제공)
    - 클래스 변수명 : 테이블의 각 필드 이름
    - Model Field
        - 데이터 베이스 테이블의 열을 나타내는 중요한 구성 요소
        - **데이터 유형**과 **제약 조건**을 정의

## Model Field

- DB 테이블의 **필드(열)**을 정의하며, 해당 필드에 저장되는 **데이터 타입**과 **제약 조건**을 정의
- Model Field 구성
    1. Field types (필드 유형)
        - 데이터베이스에 저장될 데이터의 종류를 정의
    2. Field options (필드 옵션)
        - 필드의 동작과 제약조건을 정의

### Field Types

- 데이터베이스에 저장될 데이터의 종류를 정의 (models 모듈의 클래스로 정의되어 있음.)
    - `CharField()` : 제한된 길이의 문자열을 저장 (필드의 최대 길이를 결정하는 `max_length`는 필수 옵션)
        - 내부에서 유효성 검사를 한다.
    - `TextField()` : 길이 제한이 없는 대용량 텍스트를 저장 (무한대는 아니며 사용하는 시스템에 따라 달라짐)

### Field Options

- 필드의 **동작**과 **제약조건**을 정의
- **제약조건** : 특정 규칙을 강제하기 위해 테이블의 열이나 행에 적용되는 규칙이나 제한사항
    - 숫자만 저장되도록, 문자가 100자까지만 저장되도록 하는 등..

## Migrations

- model 클래스의 **변경사항(필드 생성, 수정 삭제 등)**을 **DB에 최종 반영**하는 방법

`$ python manage.py makemigrations`  : model class 를 기반으로 최종 설계도 작성

`$ python manage.py migrate` : 최종 설계도를 DB에 전달하여 반영

**model class에 변경사항이 생겼다면 반드시 새로운 설계도를 생성하고 이를 DB에 반영해야 한다.**

## Admin site

### Automatix admin interface

- Django가 추가 설치 및 설정 없이 자동으로 제공하는 관리자 인터페이스
    - 데이터 확인 및 테스트 등을 진행하는 것에 매우 유용하다.

1. admin 설정
2. 모델 클래스 등록
3. admin site 로그인 후 확인하기
4. 데이터 생성, 수정, 삭제 테스트

※  참고

- 데이터 베이스 초기화
    1. migration 파일 삭제
        - `__init__.py` 삭제 금지
    2. db.sqlite3 삭제

- migration 관련
    - `$ python manage.py showmigrations`  :  migrations 파일들이 migrate 됐는지 안됐는지 여부 확인하는 명령어
        - X 표시가 있으면 migrate가 완료되었음을 의미
    - `$ python manage.py sqlmigrate articles 0001` : 해당 migrations 파일이 SQL 언어로 어떻게 번역되어 DB에 전달되는지 확인하는 명령어

### SQLite

- 데이터베이스 관리 시스템 중 하나
- Django의 기본 데이터 베이스로 사용된다. (파일로 존재, 가볍고 호환성이 좋음.)
