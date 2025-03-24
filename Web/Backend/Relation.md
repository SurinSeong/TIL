# Many to one Relationships

Comment

| **id** |
| --- |
| content |
| created_at |
| updated_at |
| **Article에 대한 외래키 (id)** |

Article

| **id** |
| --- |
| title |
| content |
| created_at |
| updated_at |

id = primary key

**외래키**에 올 수 있는 값 = 내가 참조하고 있는 대상의 **고유한 값** (무조건 id는 아님.)

## 댓글 모델

```python
ForeignKey(to, on_delete) # N:1 관계 설정 모델 필드
# to : 누구를 참조하는가 (참조할 대상의 클래스명)
# on_delete : 어떠한 형태로 N을 관리할 것인가 (외래키가 참조하는 객체가 사라졌을 때, 외래키를 가진 객체를 어떻게 처리할지를 정의하는 설정 => 데이터 무결성)
```

- 댓글 모델 정의
    - ForeignKey 클래스의 인스턴스 이름은 **참조하는 모델 클래스 이름의 단수형**으로 작성하는 것을 권장
    - 외래키는 ForeignKey 클래스를 작성하는 위치와 관계없이 **테이블 필드 마지막에 생성**됨.
    - on_delete
        - ‘CASCADE’ : 부모 객체(참조된 객체)가 삭제되었을 때, 이를 참조하는 객체도 삭제한다.
        - ‘PROJECTED’ : 내가 참조하고 있는 N의 객체들이 존재하고 있으면, 부모 객체를 삭제할 수 없음. (함부로 게시글을 삭제할 수 없도록 하기 위해)
- Migration 이후 댓글 테이블 확인
    - 댓글 테이블의 article_id 필드 확인
    - 참조하는 클래스 이름의 소문자(단수형)로 작성하는 것이 권장되었던 이유
        - 참조할 대상 클래스 이름 + ‘_’ + 클래스 이름

## 관계 모델 참조

### 역참조

- N:1 관계에서 1에서 N을 참조하거나 조회하는 것 (1 → N)
- N은 외래 키를 가지고 있어 물리적으로 참조가 가능하지만, 1은 N에 대한 참조 방법이 존재하지 않아 별도의 **역참조 기능**이 필요함.
- `article.comment_set.all()` : 모델 인스턴스 / related_manager(역참조 이름) / QuerySetAPI
    - 특정 게시글에 작성된 댓글 전체를 조회하는 명령
- related manager
    - N:1 혹은 M:N 관계에서 **역참조** 시에 사용하는 매니저
    - ‘objects’ 매니저를 통해 QuerySetAPI 를 사용했던 것 처럼 **related manager를 통해 QuerySet API를 사용할 수 있게 됨.**

## 응답 데이터 재구성

- 댓글 조회 시 게시글 출력 내역 변경
    - 댓글 조회 시 게시글 번호만 제공해주는 것이 아닌 **게시글의 제목까지 제공**
    - 필요한 데이터를 만들기 위한 Serializer는 내부에서 **추가 선언**이 가능하다.
- 읽기 전용 필드 지정 주의 사항
    - 특정 필드를 override 혹은 추가한 경우, read_only_fields는 동작하지 않는다.
        - 이런 경우, 새로운 필드에 read_only 키워드 인자로 작성해야 한다.
    - read_only_fields 속성과 read_only 인자
        - read_only_fields : 기존 외래 키 필드 값을 그대로 응답 데이터에 제공하기 위해 지정하는 경우
        - read_only : 기존 외래 키 필드 값의 결과를 다른 값으로 덮어쓰는 경우 / 새로운 응답 데이터 값을 제공하는 경우

## 역참조 데이터 구성

- Article → Comment  간 역참조 관계를 활용한 JSON 데이터 재구성

1. 단일 게시글 조회 시, 해당 게시글에 작성된 댓글 목록도 함께 붙여서 응답
    - **Nested Relationships** (역참조 매니저 활용)
        - 모델 관계 상으로 참조하는 대상은 **참조되는 대상의 표현에 포함되거나 중첩**될 수 있음.
        - 이러한 중첩된 관계는 **serializers 를 필드로 사용**하여 표현 가능
        
2. 단일 게시글 조회 시, 해당 게시글에 작성된 댓글 개수도 함께 붙여서 응답
    - View 로직 개선 : annotate 사용
        - View에서 Article 객체를 조회할 때 annotate를 활용해 num_of_comments  필드를 추가
            - annotate : django ORM 함수로, **SQL의 집계함수를 활용**하여 **쿼리 단계에서 데이터 가공을 수행**
            
        - 댓글 수를 세어 num_of_comments 라는 필드를 추가한다.
        - serializer.data를 반환하면, 해당 article 객체에는 num_of_comments라는 주석 필드가 포함되어 있다.
        
    - Serializer 개선 : SerializerMethodField 사용
        - SerializerMethodField는 **읽기 전용 필드를 커스터마이징** 하는 것에 사용한다.
        - 이 필드를 선언한 뒤 **get_<필드명> 메서드를 정의**하면, 해당 메서드의 반환값이 직렬화 결과에 포함된다.
        - serializer.data를 호출할 때, get_num_of_comments 메서드가 실행되어 num_of_comments 값이 자동으로 포함된다.
        - view에서 data를 딕셔너리로 변환하거나 수정할 필요 없이, **serializer.data를 바로 반환해도 최종 JSON 응답에 num_of_comments 값이 반영**된다.

- SerializerMethodField란?
    - DRF에서 제공하는 **읽기 전용 필드**
    - Serializer에서 **추가적인 데이터 가공**을 하고 싶을 때 사용
        - ex) 특정 필드 값을 조합해 **새로운 문자열 필드**를 만들거나, **부가적인 계산** (비율, 합계, 평균)을 하는 경우 등
    - 동작원리
        1. SerializerMethodField를 Serializer 클래스 내에서 필드로 선언하면, DRF는 **get_<필드명>**이라는 이름을 가진 메서드를 **자동으로 찾음**
        2. full_name = serializers.SerializerMethodField()라고 선언하면 get_full_name(self, obj) 메서드를 찾아 해당 값을 직렬화 결과에 넣어준다.
        3. obj는 현재 직렬화 중인 모델 인스턴스이고, 이 메서드에서 obj의 속성이나 annotate된 필드를 활용해 새 값을 만들 수 있다.
    - 주의사항
        - 읽기 전용으로 생성, 수정 요청 시에는 사용되지 않음
        - get_메서드는 **반드시 (self, obj) 형태로 정의**해야 하고,  obj는 **현재 직렬화 중인 모델 인스턴스**를 의미한다.
    - 사용 목적
        - 유연성 : 다양한 계산 로직을 손쉽게 추가 가능
        - 가독성 : 데이터 변환 과정을 Serializer 내부 메서드로 명확히 분히
        - 유지 보수성 : view나 model에 비해 serializer측 로직 변경이 용이
        - 일관성 : view에서 별도로 data 수정 없이도 직렬화 결과를 제어

# Many to many relationships (N:M or M:N)

- 한 테이블의 0개 이상의 레코드가 다른 테이블의 0개 이상의 레코드와 관련된 경우
    - **양쪽 모두에서 N:1의 관계를 가진다.**
- `ManyToManyField` 로 **중개 모델을 자동으로 생성**한다.

Teacher

| id |
| --- |
| name |

중개 모델

| id |
| --- |
| name |
| course_id |
| teacher_id |

Course

| id |
| --- |
| name |

Course에는 강의 제목만 저장

Teachers에는 강사 이름만 저장

⇒ 중개 모델을 통해 ID를 받아서 저장한다.

⇒ ManyToManyField !
