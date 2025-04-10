# ManytoOne Relationships

## 모델 관계

- N:1 or 1:N
    - 한 테이블의 0개 이상의 레코드가 다른 테이블의 레코드 한 개와 관련된 관계

### Comment - Article 구현하기

- `ForeignKey()` : 한 모델이 다른 모델을 참조하는 관계를 설정하는 필드
    - N : 1 관계 표현
    - DB에서 외래키로 구현
    
    ### 모델 정의
    
    - ForeignKey 클래스의 인스턴스 이름은 참조하는 모델 클래스 이름의 단수형으로 작성하는 것을 권장함.
    - 외래키는 ForeignKey 클래스를 작성하는 위치와 관계없이 테이블의 마지막 필드로 생성된다.
    - Parameter
        - to : 참조하는 모델 class 이름
        - on_delete : 외래키가 참조하는 객체(1)가 사라졌을 때, 외래키를 가진 객체(N)를 어떻게 처리할지를 정의 > 데이터 무결성
            - `CASCADE` : 참조된 객체 (부모 객체, 1)가 삭제될 때, 이를 참조하는 모든 객체도 삭제
            - `SET_NULL` : 외래키의 기본 값을 null로 바꾸기
            - `SET_DEFAULT` : 외래키의 기본 값을 원하는 것을 설정하기
    
    ### Migration 이후의 Comment
    
    - FK : `article_id` 생성
        - 내가 참조하는 모델명의 단수형으로 생성해야 구분하기 편하다.
    
    ### 댓글 생성
    
    ```python
    # Comment 클래스의 인스턴스 comment 생성
    comment = Comment()
    
    # 인스턴스 변수 저장
    comment.content = 'first comment'
    
    # DB에 댓글 저장
    comment.save()
    
    # 에러발생!!
    # IntegrityError: NOT NULL constraint failed: articles_comment.article_id
    	# NOT NULL 제약 조건에 걸림.
    	# 무언가 값이 존재하지 않음.
    		# comment.article_id 존재하지 않음.
    		
    # 게시글 조회
    article = Article.objects.get(pk=1)
    
    # 외래 키 데이터 입력
    comment.article = article
    	# pk 값을 직접 외래 키 컬럼에 넣어줄 수 도 있지만 권장하지 않는다.
    ```
    

## 관계모델 참조

- 역참조
    - N : 1 관계에서 **1에서 N을 참조하거나 조회**하는 것
    - 모델 간의 관계에서 관계를 정의한 모델이 아닌, **관계의 대상이 되는 모델에서 연결된 객체들에 접근하는 방식**
    - N은 외래키를 가지고 있어, 물리적으로 참조가 가능하지만, 1은 N에 대한 참조 방법이 존재하지 않아 별도의 역참조 키워드가 필요함.
    - `article.comment_set.all()`
    모델 인스턴스.역참조 이름 (related manager).QuerySet API
    ⇒ 특정 게시글(1)에 작성된 댓글 전체(N)를 조회하는 요청
- related manager
    - N : 1 혹은 M : N 관계에서 역참조 시에 사용하는 매니저
    - ‘objects’ 매니저를 통해 QuerySet API를 사용했던 것처럼 related manager를 통해 QuerySet API를 사용할 수 있게 된다.

### 댓글 구현 - CREATE

1. form 생성 - `CommentForm` 정의
사용자로부터 댓글 데이터를 입력 받기 위한
2. detail view 함수에서 `CommentForm`을 사용하여 detail 페이지에 렌더링
3. Commet 클래스의 article은 사용자로부터 입력받는 값이 아닌, view 함수 내에서 다른 방법으로 전달받아 저장되어야 한다.
    - article은 pk값을 이용해 받아와야 한다.
4. commentForm을 이용해 댓글 생성하기
이때, 한번에 저장하는 것이 아닌, 인스턴스 먼저 생성하고(`save(commit=False)`, 해당 게시글을 외래키로 넣어주고 **다시 진짜 DB에 저장**한다.

### 댓글 구현  - READ

- detail view  함수에서 전체 댓글 데이터 조회하기
- 역참조 매니저 사용한다.

### 댓글 구현 - DELETE

- 댓글 삭제는 보통 댓글 옆에 있다.
- 반복문 안에 url이 존재할 수 있도록 둔다.

나중에는 view 함수에서 return은 데이터만 Json 형태로 넘겨줄 수 있도록 한다.

### ※ 역참조 이름 변경

해당 모델에 -s를 붙인다.

`author = models.ForeignKey(to=Author, on_delete=models.CASCADE, related_name='books')`

참조 : 1번 게시글의 작성자 조회 N → 1

역참조 : 1번 유저가 작성한 모든 게시글 1 → N
`user.article_set.all()`

## 모델 관계 설정

1. User(1) - Article(N)
2. User(1) - Comment(N)

- User : AUTH_USER_MODEL 설정!

## View decorators

- View 함수의 동작을 수정하거나 추가 기능을 제공하는 것에 사용되는 python 데코레이터
    - 코드의 재사용성을 높이고 뷰 로직을 간결하게 유지

### Allowed HTTP methods

- 특정 HTTP method로만 View 함수에 접근할 수 있도록 제한하는 데코레이터
- 주요 Allowed HTTP methods
    1. require_http_methods([’METHOD1’, ‘METHOD2’, …])
        - 지정된  HTTP method 만 허용
        - 에러 시, 405 response (HttpResponseNotAllowed) 반환
    2. require_safe()
        - GET과 HEAD method만 허용
    3. require_POST()
        - POST method만 허용
    - require_GET 대신 require_safe를 권장하는 주요 이유
        - 웹 표준 준수
            - GET과 HEAD는 안전한 메소드로 간주된다.
        - 호환성
            - 일부 소프트웨어는 HEAD 요청에 의존
        
        ⇒ 웹 표준을 준수하고, 더 넓은 범위의 클라이언트와 호환되며, 안전한 HTTP 메소드만을 허용하는 view 함수를 구현할 수 있음.
        

## ERD (Entity-Relationship Diagram)

- 데이터베이스의 구조를 시각적으로 표현하는 도구
- Entity(개체), 속성, 그리고 엔티티 간의 관계를 그래픽 형태로 나타내어 시스템의 논리적 구조를 모델링 하는 다이어그램

### 구성요소

1. 엔티티 (Entity)
    - 데이터베이스에 저장되는 객체나 개념
2. 속성
    - 엔티티의 특성이나 성질
3. 관계
    - 엔티티 간의 연관

### Cardinality

- 한 엔티티와 다른 엔티티간의 수적 관계를 나타내는 표현
- 주요 유형
    - 일대일
    - 다대일
    - 다대다

### ERD의 중요성

- 데이터베이스 설계의 핵심 도구
- 시각적 모델링으로 효과적인 의사소통 지원
- 실제 시스템 개발 전 데이터 구조 최적화에 중요

## 추가내용

- url 설계
    - articles/<int:article_id>/comments/<int:comment_id>/delete/
        - **RESTful하게 설계**한다.
            - [ ]  RESTful이라는 것 정리하기
        - 웹 API 설계를 할 때, 리소스(자원, article_id)을 중심으로 설계한다.
        - 메서드(동작, ex) create, delete)를 사용해서 동작을 명확하게 표현한다.
        1. URL 경로는 **리소스 위주**로 설계한다. (리소스는 복수형으로 작성한다.)
        2. 계층적이고 (1 : N 관계), 의미있도록 설계 (URL만 봐도 뭐하는지 알면 좋다.)
        
        ⇒ 가독성 높음, 일관성, 유지보수, **표준**이기 때문에 확장성이 좋다. 연동하기 좋다.
        

- CASCADE : 참조 대상이 삭제되면, 연결된 객체도 삭제 (게시글이 지워지면, 게시글의 댓글이 전부 삭제)
- PROJECT : 참조 대상이 삭제되지 못하도록 막음
    - **Django ORM (QuerySet API가 실행될 때)**, 확인하고 막는다.
- RESTRICT : 참조 대상이 삭제되지 못하도록 막음
    - **SQL, 테이블 레벨**에서 실행될 때, 확인되고 막는다.

- User 모델을 참조하는 2가지 방법
    1. models.py에서는  AUTH_USER_MODEL을 참조한다.
    2. 그 외의 파일에서는 get_user_model()을 가져와 참조한다.
    
    ⇒ 왜? **앱 등록 순서대로** 모델 초기화를 한다.
    
    models.py에서 계속 로드를 하면 **순환참조에러**가 발생할 수 있다.
    

- 왜 request.user 하면 username이 나올까?
    - 클래스 매직 메서드(__ str __) 사용
 
## ※추가 내용

### Relationship

1. 1:1

- A테이블의 각 레코드가 B테이블의 하나의 레코드와 연결되고, 반대의 경우도 성립함.
- **데이터 분류, 추가 데이터, 민감한 데이터** 등 따로 관리해야 하는 경우 주로 사용함.

2. N:1

- A테이블의 하나의 레코드가 B테이블의 하나 이상 레코드와 연결
- 하지만, B테이블의 하나의 레코드는 A테이블 하나의 레코드에만 연결됨!

3. N:M

- A테이블의 하나의 레코드가 B테이블의 하나 이상의 레코드와 연결.
- 그 반대도 가능함.
- 중계 테이블!
- ex)
    - 수강 과목 : 여러명 수강 가능
    - 학생 : 여러 과목 수강 가능

- 테이블 간의 **관계**를 잘 파악하는 것이 중요함!!

  ### 데이터 베이스 정규화

  - 관계형 데이터베이스 데이터 모델의 **중복을 최소화**하고 데이터의 **일관성, 유연성**을 확보하기 위한 목적으로 데이터 **분해**하는 과정
    - 비즈니스 로직에 변화가 생기더라도 데이터 모델의 변경을 최소화할 수 있음.
    - 정규화를 진행하지 않으면 **데이터 삽입/삭제/업데이트 시 이상현상이 발생**

- 정규화 절차 (in 실무)
    - 제1정규화
        - 레코드의 데이터는 고유해야 함.
        - 레코드는 고유해야 함.
    - 제2정규화
        - 기본키가 아닌 키들은 모두 기본키에만 종속
        - 기본키는 하나의 컬럼이 아닐 수 있음. 복합 가능!
        - ex)
            - 학생 취미 테이블 >> 이름, 취미, 주소, 성별
            - 주소, 성별은 취미와는 관련이 없음, 따라서 나눠줘도 된다.
        - 기본키와 기본키가 아닌 컬럼을 나눠서 어떻게 종속되는지 확인하고 분리할지 말지 판단한다.
    - 제3정규화
        - 기본키를 제외하고 다른 키에 의해 결정되는 키를 분리
