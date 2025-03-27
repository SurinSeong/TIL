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
