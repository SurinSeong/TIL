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

## Frameword

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

- Django 프로젝트 생성하기
    - `$ django-admin startproject firstpjt .` : firstpjt 라는 이름의 프로젝트 생성 (.은 현재 디렉토리를 의미한다.)
 
- Django 서버 실행
    - `$ python manage.py runserver` : manage.py 와 동일한 경로에서 서버를 실행한다.

- 서버 확인
    - 'http://127.0.0.1:8000/' 접속 후 확인
 
## Django Design Pattern

### 개요

- **디자인 패턴**
    - 소프트웨어 설계에서 발생하는 문제를 해결하기 위한 **일반적인 해결책** (공통적인 문제를 해결하는 것에 쓰이는 형식화된 관행)

- MVC (Model, View, Controller) 디자인 패턴
    - **애플리케이션을 구조화**하는 대표적인 패턴 ('데이터' & '사용자 인터페이스' & '비즈니스 로직' 을 분리)
        - **시각적 요소**와 **뒤에서 실행되는 로직**을 서로 영향 없이, **독립적**이고 쉽게 유지 보수할 수 있는 애플리케이션을 만들기 위해

- MTV (Model, Template, View) 디자인 패턴
    - **Django**에서 **애플리케이션을 구조화**하는 패턴
        - 기존 MVC 패턴과 동일하나 단순히 명칭을 다르게 정의한 것
            - View -> Template, Controller -> View

### Project & App

- 프로젝트와 앱
    - Project 안에 app 존재

- Django project : 애플리케이션의 **집합** (DB 설정, URL 연결, 전체 앱 설정 등을 처리) 
