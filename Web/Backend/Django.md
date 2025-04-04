# Django

## Web Application

- Web application 개발
    - 인터넷을 통해 사용자에게 제공되는 **소프트웨어 프로그램을 구축**하는 과정
    - 다양한 디바이스(모바일, 태블릿, PC 등)에서 웹 브라우저를 통해 접근하고 사용할 수 있음.

### 클라이언트와 서버

- 웹의 동작 방식
    - 우리가 컴퓨터 혹은 모바일 기기로 웹 페이지를 보게 될 때까지..
    - CLIENT -> SERVER : requests (요청)
    - SERVER -> CLIENT : responses (응답)
 
- Client 클라이언트 : **서비스를 요청**하는 주체 (웹 사용자의 인터넷이 연결된 장치, 웹 브라우저)
- Server 서버 : 클라이언트의 **요청에 응답**하는 주체 (웹 페이지, 앱을 저장하는 컴퓨터)

- 우리가 웹 페이지를 보게 되는 과정
    1. 웹 브라우저(**클라이언트**)에서 'google.com'을 입력
    2. 브라우저는 인터넷에 연결된 전세계 어딘가에 있는 구글 컴퓨터(**서버**)에게 'Google 홈페이지.html' 파일을 달라고 요청
    3. 요청을 받은 구글 컴퓨터는 **데이터베이스**에서 'Google 홈페이지.html' 파일을 찾아 **응답**
    4. 전달받은 'Google 홈페이지.html' 파일을 사람이 볼 수 있도록 웹 브라우저가 해석해주면서 사용자는 구글의 메인 페이지를 보게 된다.
 
### Backend & Frontend

- 웹 개발에서의 Frontend와 Backend
    - Frontend 프론트엔드
        - **사용자 인터페이스**(UI)를 구성하고, 사용자가 **애플리케이션과 상호작용**할 수 있도록 함  
        => HTML, CSS, JavaScript, 프론트엔드 프레임워크 등

    - Backend 백엔드
        - **서버** 측에서 동작하며, 클라이언트의 **요쳥에 대한 처리**와 **데이터베이스와의 상호작용** 등을 담당  
        => 서버 언어 (Python, Java 등) 및 백엔드 프레임워크, 데이터베이스, API, 보안 등

## Framework

### Web Framework

- **웹 서비스 개발**에는 무엇이 필요할까?
    - 로그인, 로그아웃, 회원 관리, 데이터 베이스, 보안 등.. 많은 기술이 필요하다.
    - 하나부터 열까지 개발자가 모두 작성하는 것은 현실적으로 어렵다.
        - 하지만 모든 것을 직접 만들 필요가 없음. (**잘 만들어진 것**을 가져와 **좋은 환경에서 내 것으로 잘 사용하는 것**도 능력!)

- Web Framework
    - 웹 애플리케이션을 빠르게 개발할 수 있도록 도와주는 도구
        - **개발에 필요한 기본 구조**, **규칙**, **라이브러리** 등을 제공
     
### Django Framework

- django : Python 기반의 대표적인 웹 프레임워크

- Django를 사용하는 이유
    - 다양성 : Python 기반으로 소셜 미디어 및 빅데이터 관리 등 **광범위한 서비스 개발**에 적합
    - 확장성 : 대량의 데이터에 대해 **빠르고 유연하게 확장**할 수 있는 기능을 제공
    - 보안 : **취약점으로부터 보호하는 보안 기능**이 기본적으로 내장되어 있음
    - 커뮤니티 지원 : 개발자를 위한 지원, 문서 및 업데이트를 제공하는 **활성화된 커뮤니티**

- 검증된 웹 프레임워크
    - **대규모 서비스**에서도 안정적인 서비스 제공
    => ex) Spotify, Instargram, Dropbox, Delivery Hero

### 가상 환경

- 가상 환경 : Python 애플리케이션과 그에 따른 패키지들을 격리하여 관리할 수 있는 **독립적인** 실행 환경

- 환경 구조 예시
    - **Python Global 환경** 안에, 가상 환경 A, 가상 환경 B가 존재하고, **각각의 가상 환경에는 서로 다른 버전의 라이브러리가 존재**한다.

- 가상 환경 만들어보기

    1. 가상 환경 venv 생성
        `$ python -m venv venv`
    
    2. 가상 환경 활성화
        `$ source venv/Scripts/activate`
    
    3. 환경에 설치된 패키지 목록 확인
        `$ pip list`
        - 패키지 목록이 필요한 이유 : 프로젝트를 위해 어떤 버전을 설치해서 사용했는지에 대한 패키지 목록이 공유되어야 **오류를 방지**할 수 있다.
    
        - **의존성 패키지**
            - 한 소프트웨어 패키지가 다른 패키지의 기능이나 코드를 사용하기 때문에, **그 패키지가 존재해야만 제대로 작동**하는 관계
            - 사용하려는 패키지가 설치되지 않았거나, 호환되는 버전이 아니면 **오류가 발생**하거나 **예상치 못한 동작**을 보일 수 있음.
            - `requests` 설치 후 설치되는 **패키지 목록 변화** 확인하기! (단순하게 하나만 설치되는 것이 아니다!)
    
    4. 의존성 패키지 목록 생성
        `$ pip freeze > requirements.txt`

- 의존성 패키지 관리의 중요성
    - 개발 환경에서는 **각각의 프로젝트가 사용하는 패키지**와 **그 버전을 정확하게 관리**하는 것이 중요하다.
 
※ 패키지 목록 기반 설치

- 처음부터 'requirements.txt'를 받은 상태로 진행하는 경우, **가상환경 활성화 후 'requirements.txt' 기반으로 패키지 설치가 필요**
    - 가상환경 폴더 venv는 .gitignore에 의해 공유되지 않음.  
`$ pip install -r requirements.txt`

### Django Project

- Django 프로젝트 생성 전 루틴

    1) 가상환경 생성
    2) 가상환경 활성화
    3) Django 설치
    4) 의존성 파일 생성 (패키지 설치 시마다 진행)  
    ※ Python 3.10 이상일 경우, Django 5 버전이 설치되기 때문에 주의!

- **Django 프로젝트 생성**하기
    - `$ django-admin startproject firstpjt .` : firstpjt 라는 이름의 프로젝트 생성 (.은 현재 디렉토리를 의미한다.)
    - **who : django-admin / what : firstpjt / how : startproject / where : .**
 
- Django **서버 실행**
    - `$ python manage.py runserver` : manage.py 와 동일한 경로에서 서버를 실행한다.

- 서버 확인
    - 'http://127.0.0.1:8000/' 접속 후 확인

※ render 함수

- 주어진 템플릿은 주어진 컨텍스트 데이터와 결합하고 렌더링된 텍스트와 함께 `HttpResponse` 응답 객체를 반환하는 함수
1. request
    - 응답을 생성하는 데 사용되는 요청 객체
2. template_name
    - 템플릿 이름의 경로
3. contetx
    - 템플릿에서 사용할 데이터 (딕셔너리 타입으로 작성)
 
## Django Design Pattern

### 개요

- **디자인 패턴**
    - 소프트웨어 **설계**에서 발생하는 문제를 해결하기 위한 **일반적인 해결책** (공통적인 문제를 해결하는 것에 쓰이는 형식화된 관행)
    - "**애플리케이션의 구조는 이렇게 구성하자**" 라는 관행

- MVC (**Model, View, Controller**) 디자인 패턴
    - **애플리케이션을 구조화**하는 대표적인 패턴 ('데이터(Model)' & '사용자 인터페이스(View)' & '비즈니스 로직(Controller)' 을 분리)
        - **시각적 요소**와 **뒤에서 실행되는 로직**을 서로 영향 없이, **독립적**이고 쉽게 유지 보수할 수 있는 애플리케이션을 만들기 위해

- MTV (Model, Template, View) 디자인 패턴
    - **Django**에서 **애플리케이션을 구조화**하는 패턴
        - 기존 MVC 패턴과 동일하나 단순히 명칭을 다르게 정의한 것
            - View -> Template, Controller -> View
         
    - **Model** : data를 어떻게 다룰 것 인지 / 필요로 하는 데이터가 어떻게 구성되고, 어떤 관계를 맺고 있는지 / 데이터 조회, 수정, 삭제, 저장을 위해 거치기 위한 과정은?
    - **View** : 클라이언트가 어떠한 요청을 보내게 된다면, 서버는 그에 맞는 응답을 보낸다. (서버의 역할). 이때, 요청에 적합한 응답을 보내기 위한 로직을 작성하는 영역.
    - **Template** : 사용자가 바라보는 모습

### Project & App

- 프로젝트와 앱
    - Project 안에 app 존재

- Django project : 애플리케이션의 **집합** (DB 설정, URL 연결, 전체 앱 설정 등을 처리)
- Django application : 독립적으로 작동하는 **기능 단위** 모듈
    - 각자 특정한 기능을 담당하며 다른 앱들과 함께 하나의 프로젝트를 구성한다.
    - 예시) 온라인 커뮤니티 카페를 만든다면??
        - 프로젝트 : OO카페 (전체 설정 담당)
        - 프로젝트 구성을 위해 필요한 것
            - 게시글 **기능**을 담당하는 어플리케이션
            - 댓글 **기능**을 담당하는 어플리케이션 (or 게시글 어플리케이션에 기능 추가 가능)
            - 회원 관리 **기능**을 담당하는 어플리케이션
         
- **앱을 사용하기 위한 순서**
    
    1. 앱 생성
        - 앱의 이름은 복수형으로 지정하는 것을 권장함.  
          `$ python manage.py startapp articles`  
          프로젝트 관리자 : manage.py  
          하고 싶은 것 : startapp (어플리케이션 만들기)  
          어플리케이션 이름 : articles (게시글의 전반적인 기능 담당) 
          
    2. 앱 등록
        - 반드시 앱을 **생성한 후에 등록**해야 한다.
      
        - setting.py : 프로젝트 설정 파일
            - INSTALLED_APPS에 등록을 원하는 어플리케이션명 넣어주기
         
    - 프로젝트를 생성했을 때 기본적으로 만들어지는 폴더 관련
        - setting.py : 기본적인 설정에 관한
        - urls.py : 사용자의 요청에 대한 대응 관련
        - wsgi.py : 배포 진행할 때, 장고에 들어오는 요청을 한번에 처리할 수 있도록 하는
        - asgi.py : 비동기식 웹서버 관련
        - __init__.py : 해당 프로젝트를 **패키지로** 인식할 수 있도록 하는
     
    - 어플리케이션을 생성했을 때 기본적으로 만들어지는 폴더 관련
        - admin.py : 관리자용
        - models.py
        - views.py : http에 대한 응답을 처리
        - apps.py : app의 기본적인 정보가 작성되는
        - tests.py : 프로젝트 테스트 코드 작성하는 (TDD 검색해서 웹서비스 개발에 관한 테스트 확인)
     
## RESTAPI

- API : 두 소프트웨어가 **서로 통신**할 수 있게 하는 메커니즘
    - 클라이언트 <-> 서버 처럼 서로 다른 프로그램에서 요청과 응답을 받을 수 있도록 만든 체계
 
- Web API
    - 웹 서버 또는 웹 브라우저를 위한 API
    - 대표적인 Third Party Open API 서비스 목록
        - Youtube API
        - Google Map API
        - Naver Papago API
        - Kakao Map API
     
- REST (Representational State Transfer) : API Server를 개발하기 위한 일종의 소프트웨어 설계 **방법론**

- RESTful API
    - **REST 원리를 따르는 시스템**을 RESTful 하다고 부른다.
    - **자원을 정의**하고 **자원에 대한 주소를 지정**하는 전반적인 방법을 서술
        - 각각 API 서버 구조를 작성하는 모습이 너무 다르니 어느정도 **약속을 만들어서 다같이 API 서버를 구성**하자!
     
- REST 에서 자원을 사용하는 방법
    1. 자원의 식별 : URI
    2. 자원의 행위 : HTTP Methods
    3. 자원의 표현 : JSON 데이터
 
### 자원의 식별

- URI (Uniform Resource Identifier : 통합 자원 식별자) : 인터넷에서 **리소스(자원)를 식별**하는 문자
    - URL의 상위 개념
    - URL과 동등한 위치의 또다른 것 : URN
 
- RESTful 한 API를 구축하기 위해 **URL**이 필요하다.
- URL (Uniform Resource Locator : 통합 자원 위치) : 웹에서 주어진 리소스의 주소
    - 네트워크 상에 **리소스가 어디 있는지**를 알려주기 위한 약속
    - 즉, 어디에 요청을 보내야 하는가를 URL을 통해 작성한다.
    - 예시) http://www.example.com:80/path/to/myfile/html?key1=value1&key2=value2#SomewhereInTheDocument
        - http : Scheme (구조) >> 웹서비스가 아니라면 다른 명칭을 사용할 수 있다.
        - www.example.com : Domain Name >> 요청의 기본이 되는 주소 (정확한 식별 위치)
            - 구매해 사용할 수 있음.
        
        - :80 : Port >> 동일한 도메인명이지만, 포트 번호에 따라 요청의 응답처리 방법이 달라진다.
            - 예시) django의 port 번호 : 8000 / vue의 port 번호 : 5173
                - 두 서버는 동일한 도메인명(127.0.0.1)을 가짐.
                - 이때, port 번호만 바꿔주면 나눠서 요청을 보낼 수 있다.
            
            - 배포를 할 때 사용하게 될 구역
         
        - /path/to/myfile/html : **Path** to the file (실제 파일의 위치)
            - 기능을 구현하면서 직접적으로 수정을 하게 될 구역
        - ?key1=value1&key2=value2 : **Parameters**
            - 기능을 구현하면서 직접적으로 수정을 하게 될 구역
        
        - #SomewhereInTheDocument : Anchor
            - 북마크 (많은 문서 내부의 특정 영역)
         
### 자원의 행위

- HTTP Requests **Methods** : 리소스에 대한 행위 (수행하고자 하는 동작)를 정의
    - **HTTP verbs** 라고도 한다.
 
- 대표 HTTP Requests Methods
    1. GET (조회 요청)
        - 서버에 리소스의 표현을 **요청**한다.
        - GET을 사용하는 요청은 데이터만 검색해야 한다.
    
    2. POST (생성)
        - 데이터를 지정된 리소스에 **제출**
        - 서버의 **상태를 변경**
        - 주로 **생성**의 역할을 맡는다.
    
    3. PUT/PATCH (수정)
        - 요청한 주소의 리소스를 **수정**
        - PUT, PATCH의 차이점 : 일정 부분만 수정 or 전체 수정
    
    4. DELETE
        - 지정된 리소스를 **삭제**
      
- HTTP response status codes : 특정 HTTP **요청이 성공적으로 완료**되었는지 여부를 나타냄
    - 5개의 응답 그룹
        - Informational responses (100-199)
        - Successful responses (200-299) *
        - Redirection messages (300-399)
        - Client error responses (400-499) *
        - Server error responses (500-599) *
     
### 자원의 표현

- 현재 Django가 응답(자원을 표현)하는 것
    - Django는 Full stack framework에 속하기 때문에 기본적으로 **사용자에게 페이지 (html)를 응답**
    - 하지만 서버가 응답할 수 있는 것은 페이지 뿐만이 아니라 다양한 데이터 타입을 응답할 수 있다.
    - REST API는 이 중에서도 **JSON** 타입으로 **응답하는 것**을 권장한다.
 
- 우리가 해야 할 것은 서버가 응답해줄 json을 어떻게 구축할 것인가?

## 요청과 응답

### DRF (Django REST framework)

- Django에서 Restful API 서버를 쉽게 구축할 수 있도록 도와주는 오픈소스 라이브러리

### Django URLs

- 사용자가 어떠한 경로로 요청을 보내게 되면, 그 요청에 대한 우선적인 처리를 urls.py가 체크한다.
- 요청에 맞는 함수를 호출한다.
- 적절한 input에 대한 output을 반환한다.

- URL dispatcher (운항 관리자, 분배기)
    - URL 패턴을 정의하고, 해당 패턴이 일치하는 요청을 처리할 view 함수를 연결 (매핑)
    - 식별자 : urls.py / method : decorator / 형식 : JSON
 
### 변수와 URL

- 현재 URL 관리의 문제점 : 템플릿의 많은 부분이 중복되고, URL의 일부만 변경되는 상황이라면 계속해서 비슷한 URL과 함수를 작성해 나가야할까?
- **Variable Routing** : URL 일부에 변수를 포함시키는 것 (변수는 view 함수의 인자로 전달할 수 있다.)
    - path_converter
        - 형식 : <type: variable_name>
     
- 두 번째 어플리케이션 (pages)을 만들게 된다면?? + 그 안에 다른 어플리케이션과 동일한 이름의 함수가 들어 있다면?
    - 각 app 마다의 url을 각자의 app 폴더 내에서 관리하도록 하는 기능이 존재함!
