# SQL

- 데이터베이스 : 체계적인 데이터 모음
- 데이터 : 저장이나 처리에 효율적인 형태로 변환된 정보

**데이터를 저장하고 잘 관리하여 활용할 수 있는 기술이 중요해짐!**

## Relational Database

- 데이터베이스 역할 : 데이터를 저장 (구조적 저장) 하고 조작 (CRUD)
- 관계형 데이터베이스 : 데이터 간에 **관계**가 있는 데이터 항목들의 모음
    - 테이블, 행, 열의 정보를 구조화하는 방식
    - **서로 관련된 데이터 포인터를 저장**하고 이에 대한 **액세스**를 제공
 
- 관계 : 여러 테이블 간의 (논리적) 연결
    - 관계로 할 수 있는 것 : 이 관계로 인해 두 테이블을 사용하여 데이터를 다양한 형식으로 조회할 수 있음.

- 관계형 데이터베이스 관련 키워드

1. Table (Relation)

    - 데이터를 기록하는 곳

2. Field (Column, Attribute)

    - 각 필드에는 고유한 데이터 형식(타입)이 지정됨
  
3. Record (Row, Tuple)

    - 각 레코드에는 구체적인 데이터 값이 저장됨.

4. Database (Schema)

    - 테이블의 집합
  
5. Primary Key (기본 키, PK)

    - 각 레코드의 고유한 값
    - 관계형 데이터베이스에서 **레코드의 식별자**로 활용
  
6. Foreign Key (외래 키, FK)

    - 테이블의 필드 중 다른 테이블의 레코드를 식별할 수 있는 키
    - 다른 테이블의 기본 키를 참조
    - 각 레코드에서 서로 다른 테이블 간의 **관계를 만드는 데** 사용
  
## DBMS (Database Management System)

- 데이터베이스를 관리하는 소프트웨어

    - 데이터 저장 및 관리를 용이하게 하는 시스템
    - 데이터베이스와 사용자 간의 인터페이스 역할
    - 사용자가 데이터 구성, 업데이트, 모니터링, 백업, 복구 등을 할 수 있도록 도움
 
- RDBMS : 관계형 데이터베이스를 관리하는 소프트웨어 프로그램

    - 서비스 종류

        - SQLite : 경량의 오픈 소스 데이터베이스 관리 시스템
     
            - 컴퓨터나 모바일 기기에 내장되어 간단하고 효율적인 데이터 저장 및 관리를 제공
  
        - MySQL
        - PostgreSQL
        - Oracle Database
     
## SQL (Structure Query Language)

- 데이터베이스에 정보를 저장하고 처리하기 위한 프로그래밍 언어
- 테이블 형태로 **구조화**된 관계형 데이터베이스에게 요청을 **질의**

- SQL Syntax

1. SQL 키워드는 대소문자를 구분하지 않음

    - 하지만 대문자로 작성하는 것을 권장 (명시적 구분)
  
2. 각 SQL Stamements의 끝에는 세미콜론(';')이 필요

    - ;은 각 SQL Statements을 구분하는 방법 (명령어의 마침표)

### SQL Statement

- SQL을 구성하는 가장 기본적인 코드 블록

```
SELECT column_name FROM table_name;
```

- 수행 목적에 따른 SQL Statements 4가지 유형

1. DDL - 데이터 정의
2. DQL - 데이터 검색
3. DML - 데이터 조작
4. DCL - 데이터 제어

### SELECT

- 테이블에서 데이터를 조회 및 반환
- '*'를 사용하여 모든 필드 선택

```
SELECT
    select_list
FROM
    table_name;
```

- SELECT 키워드 이후, 데이터를 선택하려는 필드를 하나 이상 지정
- FROM 키워드 이후, 데이터를 선택하려는 데이블의 이름을 지정

---

## DDL

### CREATE TABLE

- CREATE TABLE syntax

    - 각 필드에 적용할 데이터 타입 작성
    - 테이블 및 필드에 대한 제약조건(constraints) 작성
 
```
CREATE TABLE table_name (
    column_1 data_type constraints,
    column_2 data_type constraints,
    ...,
)
```

- 테이블 구조 (schema) 확인

`PRAGMA table_info('테이블명')`  

※ cid
    - Column ID를 의미, 각 컬럼의 고유한 식별자를 나타내는 정수 값
    - 직접 사용하지 않고, PRAGMA 명령과 같은 메타 데이터 조회에서 출력 값으로 활용된다.

- SQLite 데이터 타입

1. NULL

    - 아무런 값도 포함하지 않음을 나타낸다.

2. INTEGER

    - 정수

3. REAL

    - 부동 소수점

4. TEXT

    - 문자열

5. BLOB

    - 이미지, 동영상, 문서 등의 바이너리 데이터

- Constraints (제약조건) : 테이블의 필드에 적용되는 규칙 또는 제한 사항

    - 데이터의 무결성을 유지하고 데이터베이스의 일관성을 보장함.
    - 대표 제약 조건 3가지
    
        - `PRIMARY KEY`
        
            - 해당 필드를 기본 키로 지정 (※ INTEGER 타입에만 적용된다. INT, BIGINT 등과 같은 다른 정수 유형은 적용되지 않는다.)
         
        - `NOT NULL`
     
            - 해당 필드에 NULL 값을 허용하지 않도록 지정
      
        - `FOREIGN KEY`

            - 다른 테이블과의 외래 키 관계를 정의

        - `AUTOINCREMENT`
            
            - 자동으로 고유한 정수 값을 생성하고 할당하는 필드 속성
                
                - 필드의 자동 증가를 나타냄.
           
            - Django 기본 설정
            - 주로 primary key 필드에 적용
            - 항상 새로운 레코드에 대해 이전 최대 값보다 큰 값을 할당한다.
            - 삭제된 값은 무시되고 재사용할 수 없다.

---

### ALTER TABLE

- 테이블 및 필드 조작

1. `ALTER TABLE ADD COLUMN` syntax

    - `ADD COLUMN` 키워드 이후, 추가하고자 하는 새 필드 이름과 데이터 타입 및 제약 조건 작성
    - 단, 추가하고자 하는 필드에 NOT NULL 제약 조건이 있을 경우, **NULL이 아닌 기본 값 설정 필요**
        
        - `DEFAULT ''`
    
    - sqlite는 단일 문을 사용해서 한번에 여러 열을 추가하는 것을 지원하지 않음. 하나씩 컬럼 생성해야 한다.

2. `ALTER TABLE RENAME COLUMN` syntax

    - `RENAME COLUMN` 키워드 뒤에 이름을 바꾸려는 필드의 이름을 지정하고 `TO` 키워드 뒤에 새 이름 지정.
  
3. `ALTER TABLE DROP COLUMN` syntax

    - `DROP COLUMN` 키워드 뒤에 삭제할 필드 이름 지정
  
4. `ALTER TABLE RENAME TO` syntax

    - `RENAME TO` 키워드 뒤에 새로운 테이블 이름 지정

### DLOP TABLE

- 테이블 삭제
- `DROP TABLE` 이후 삭제할 테이블 이름 작성

---

## DML

### INSERT

- 테이블 레코드 삽입
- `INSERT INTO` 절 다음에 테이블 이름과 괄호 안에 필드 목록 작성
- `VALUES` 키워드 다음 괄호 안에 해당 필드에 삽입할 값 목록 작성
- 여러 값을 한번에 넣을 수 있음.
- 현재 날짜 생성 >> "sqlite documents date time field" 검색

```
INSERT INTO table_name (c1, c2, ...)
VALUES (v1, v2, ...);
```

### UPDATE

- 테이블 레코드 수정
- `SET` 절 다음에 수정할 필드와 새 값을 지정
- `WHERE` 절에서 수정할 레코드를 지정하는 조건 작성
- `WHERE` 절을 작성하지 않으면 모든 레코드를 수정

```
UPDATE table_name
SET column_name = expression,
[WHERE condition];
```

### DELETE

- 테이블 레코드 삭제
- `DELETE FROM` 절 다음에 테이블 이름 작성
- `WHERE` 절에서 삭제할 레코드를 지정하는 조건 작성
- `WHERE` 절을 작성하지 않으면 모든 레코드를 삭제

```
DELETE FROM table_name
[WHERE condition];
```

## Multi table queries

### JOIN

- 관계 : **여러** 테이블 간의 (논리적) 연결
- 관계의 필요성
    - 테이블 간의 관게를 잘 생각하고 외래키를 부여해야 한다.
    - **N:1의 관계에서는 1의 하나의 키를 N에서 참조한다.**

- `JOIN`이 필요한 순간

    - 테이블을 분리하면 데이터 관리는 용이해질 수 있지만, 출력 시에는 문제가 있다.
    - 테이블을 한 개만 출력할 수 밖에 없기 때문에 **다른 테이블과 결합해 출력하는 것**이 필요해진다.
    - 이때 사용하는 것이 **JOIN** 이다.
 
- `JOIN` clause : 둘 이상의 테이블에서 데이터를 검색하는 방법
- `INNER JOIN` clause : **두 테이블에서 값이 일치**하는 레코드에 대해서만 결과를 반환

    - `FROM` 절 이후 메인 테이블 지정 (`table_a`)
    - `INNER JOIN`절 이후 메인 테이블과 조인할 테이블 (`table_b`) 을 지정
    - `ON` 키워드 이후 조인 조건을 작성
    - 조인 조건은 `table_a`와 `table_b` 간의 레코드를 일치시키는 규칙을 지정
 
    ```
    SELECT select_list
    FROM table_a
    INNER JOIN table_b
    ON table_b.fk = table_a.pk;
    ```

- `LEFT JOIN` clause : 오른쪽 테이블의 일치하는 레코드와 함께 왼쪽 테이블의 모든 레코드 반환

    - `FROM` 절 이후, 왼쪽 테이블 지정 (`table_a`)
    - `LEFT JOIN` 절 이후, 오른쪽 테이블 지정 (`table_b`)
    - `ON` 키워드 이후, 조인 조건을 작성
        
        - 왼쪽 테이블의 각 레코드를 오른쪽 테이블의 모든 레코드와 일치시킴

    ```
    SELECT select_list
    FROM table_a
    LEFT JOIN table_b
    ON table_b.fk = table_a.pk;
    ```

    - 특징
        
        - 왼쪽 테이블의 모든 레코드 표기
        - 오른쪽 테이블과 매칭되는 레코드가 없으면 NULL 표시
     
## ※ 참고

### 타입 선호도 (Type Affinity)

- 컬럼에 데이터 타입이 명시적으로 지정되지 않았거나 지원하지 않을 때, SQLite가 자동으로 데이터 타입을 추론하는 것

- 목적
1. 유연한 데이터 타입 지원

    - 데이터 타입을 명시적으로 지정하지 않고도 데이터를 저장하고 조회할 수 있음.
    - 컬럼에 저장되는 값의 특성을 기반으로 데이터 타입을 유추

2. 간편한 데이터 처리

    - INTEGER type Affinity를 가진 열에 문자열 데이터를 저장해도 SQLite는 자동으로 숫자로 변환하여 처리
  
3. SQL 호환성

    - 다른 데이터베이스 시스템과 호환성을 유지
  













