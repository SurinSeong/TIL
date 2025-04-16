# DRF

## REST API

- API (Application Programming Interface) : 두 소프트웨어가 서로 통신할 수 있게 하는 메커니즘
    - **클라이언트-서버처럼 서로 다른 프로그램에서 요청과 응답을 받을 수 있도록 만든 체계**

## API 역할

- 예를 들어, 우리집 냉장고에 전기를 공급해야 한다고 가정
    - 우리는 그냥 냉장고의 플러그를 소켓에 꽂으면 제품이 작동함.
    - 중요한 것은 우리가 가전 제품에 "전기를 공급하기 위해 직접 배선을 하지 않는다."
    - 이는 매우 위험하면서도 비효율적임  
    => 복잡한 코드를 추상화하여 대신 사용할 수 있는 몇 가지 더 쉬운 구문 제공

## REST (Representational State Transfer)

- API Server를 개발하기 위한 일종의 소프트웨어 설계 방법론  
=> API Server를 설계라는 구조가 서로 다르니 이렇게 맞춰서 하는 것이 어때?

### RESTful API

- REST라는 설계 디자인 약속을 지켜 구현한 API
- REST 원리를 따르는 시스템을 RESTful하다고 부른다.
- **자원(데이터)를 어떻게 정의**?, **지원에 대한 주소를 어떻게 지정**?  
=> 각각 API 서버 구조를 작성하는 모습이 다르니깐 어느 정도 약속을 만들어서 다같이 통일해서 쓰자

### REST에서 자원을 정의하고 주소를 지정하는 방법

1. 자원의 '식별'
    
    - URI (Uniform Resource Identifier, 통합 자원 식별자)
    - 웹에서 **자원을 구별하기 위한 주소**가 필요하다.
    - URI > URL (URI가 URL보다 넓은 범위)
        
        - URL : 통합 자원 위치
        - **네트워크 상에 리소스가 어디 있는지 알려주기 위한 약속**
        
        1. Schema (or Protocol)
            - 브라우저가 리소스를 요청하는 데 사용하는 규약
            - URL의 첫 부분은 브라우저가 어떤 규약을 사용하는지를 나타낸다.
            - 기본적으로 웹은 http(s(=security))를 요구한다.
                - 메일을 열기 위한 mailto:, 파일을 전송하기 위한 ftp: 등 다른 프로토콜도 존재한다.
        
        2. Domain name
            - 요청 중인 웹 서버를 나타냄
            - 어떤 웹 서버가 요구되는 지를 가리키며 직접 IP 주소를 사용하는 것도 가능하지만, 사람이 외우기 어렵기 때문에 주로 Domain Name으로 사용
                - ex) 도메인 google.com의 IP 주소 = 142.251.42.142

        3. Port
            - 웹 서버의 **리소스에 접근하는 것에 사용되는 기술적인 문 (Gate)**
                - 우리가 웹 서핑을 할 때는 사용하지 않음. (표준 포트만 작성 시, 생략 가능)
            - HTTP 프로토콜의 표준 포트
                - HTTP : 80
                - HTTPS : 443

        4. Path
            - 웹 서버의 리소스 경로 (원하는 자원이 있는 곳)
            - 초기에는 실제 파일이 위치한 물리적 위치를 나타냈지만, 오늘날은 실제 위치가 아닌 추상화된 형태의 구조를 표현한다.
                - ex) `articles/create/`라는 주소가 실제 articles 폴더 안의 create 폴더 안을 나타 내는 것은 아님.

        5. Parameters
            - **웹 서버에 제공하는 추가 데이터**
            - `&` 기호로 구분되는 key-value 쌍 목록
            - **GET 방식으로 전송**할 때, 파라미터 형식으로 전송된다.
            - 서버는 리소스를 응답하기 전에 이러한 파라미터를 사용하여 추가 작업을 수행할 수 있음.

        6. Anchor
            - 일종의 **북마크**를 나타내며 브라우저 해당 지점에 있는 콘텐츠를 표시한다.
            - `#` : 브라우저가 컨트롤 (서버와는 관련 없음. 서버에 전송하지도 않음.)


2. 자원의 '행위'
    - HTTP request methods (= HTTP verbs) (GET, POST, ...) : 리소스에 대한 행위 (수행하고자 하는 동작)을 정의
        1. GET
            - 서버에 리소스의 표현을 요청
            - GET을 사용하는 요청은 **데이터만 검색**(**조회**)해야 한다.
        
        2. POST
            - 데이터를 지정된 **리소스에 제출** (**생성**)
            - 서버의 상태를 변경
        
        3. PUT
            - 요청한 주소의 리소스를 **수정**
        
        4. DELETE
            - 지정된 리소스를 **삭제**

    - HTTP response status code : 특정 HTTP 요청이 성공적으로 완료되었는지 여부를 나타냄
        - 100-199 : Informational responses
        - 200-299 : Successful responses
        - 300-399 : Redirection messages
        - 400-499 : Client error responses
        - 500-599 : Server error responses

3. 자원의 '표현'
    - JSON 데이터 (궁극적으로 표현되는 데이터 결과물)

---

## django REST framework

- django에서 RESTful API 서버를 쉽게 구축할 수 있도록 도와주는 오픈소스 라이브러리
- djangorestframework 설치 필요 [Django REST framework](https://www.django-rest-framework.org/)