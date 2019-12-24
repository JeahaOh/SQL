# SQL
DB와 SQL 복습  
DB, SQL 정의  
Oracle -> PostgreSQL -> MariaDB

# **Database(DB)?**
데이터의 집합, 검색 수정 삭제 추가등 관리.  
  
## 파일 시스템의 문제점 해결
- 데이터의 종속
- 데이터의 중복
  - 일관성 - 동일성을 유지하기 위해 데이터 중복을 피하기 위해
  - 보안성 - 동일한 수준에서 보안 유지
  - 경제성 - 저장되는 공간에 대한 비용 절감
  - 무결성 - 데이터의 정확성을 유지

## DB의 정의 
- 통합된 데이터 (Integrated Data)
  - 원칙적으로 데이터 중복되어 있지 않게함
- 저장된 데이터 (Stored Data)
  - 기억장치에 저장된 데이터
- 운영 데이터 (Operational Data)
  - 존재 목적이 명확하고 유용성을 지니고 있음
- 공용 데이터 (Shared Data)
  - 여러 사용자들이 서로 다른 목적으로 공유가 가능한.

## DB의 특징
실시간 접근성, 지속적인 변화, 동시 공유, 내용에 대한 참조

## 데이터베이스 관리시스템 (DBMS : DataBase Management System)
효율적으로 관리하고 검색할 수 있는 환경을 제공, 체계적인 활용을 가능케함.  
응용프로그램과 데이터베이스의 중계  
  
## 관계형 데이터베이스 관리 시스템
일반적인 DB, 작성과 이용이 편함, 응용프로그램을 변경하지 않아도 참삭이 편함.  
정보들을 Table형태로 저장함.  
테이블은 2차원 형태의 표처럼 row(행), column(열)로 구성.  
  
Table ; 표  
| Row \ Table | Column | Column | Column |
|-------------|--------|--------|--------|
|     Num     |   1    |   2    |   3    |
|  Eng  Char  |   a    |   b    |   c    |
|  Kor  Char  |   ㄱ   |   ㄴ    |   ㄷ    |
  
[참고](https://ko.wikipedia.org/wiki/데이터베이스_관리_시스템)  
  
  
# SQL? (Structured Query Language)
사용자와 관계형 데이터베이스를 연결시켜주는 표준 검색언어.  
쉽게 얘기해서 데이터베이스를 다루기위해 디자인된 언어임.  
  
프로그래밍 언어는 아니지만 Java 등 다른 프로그래밍 언어보다 더 많이 사용됨.  
테이블을 비롯한 객체(시퀀스, 인덱스 등)을 생성, 제어하는 역할.  
관계형 DB의 ANSI 표준 언어.  
  
## SQL의 종류
- DQL (Data Query Language; 질의어)
  - SELECT
  
- DML (Data Manipulation Language; 데이터 조작어)
  - INSERT
  - UPDATE
  - DELETE
  
- DDL (Data Definition Language; 데이터 정의어)  
  DB **테이블**의 생성, 수정, 삭제 (정의)하기 위한 언어  
  - CREATE
  - ALTER
  - DROP
  - RENAME
  - TRUNCATE

- TCL (Transaction Control Language; 트랜젝션 처리어)
  - COMMIT    : 트랜젝션의 정상적인 종료 처리
  - ROLLBACK  : 트랜젝션 취소
  - SAVEPOINT : 트랜젝셩 내 임시 저장지점 설정

- DCL (Data Control Language: 데이터 제어어)
  - GRANT   : DB에 대한 권한 부여
  - REVOKE  : DB에 대한 권한 박탈

# DB 설치 없이 Oracle DB 실습하기.
SQL에서 부족한 점이 느껴져서 공부 하려고 했는데 Oracle DB를 어디에 설치할지 고민이였음,  
**BUT!!** Oracle에서 설치 없이 SQL을 돌릴 수 있는 웹 기반 서비스가 있었음..  
당연히 오라클 계정이 있어야 함.  
[https://livesql.oracle.com/](https://livesql.oracle.com/)  

세션, 쿠키, JS 기반으로 테이블과 데이터들을 정의하고, 일정 시간이 지나면 데이터가 삭제 되는 듯?

Oracle 테스트 데이터인 HR을 사용하고 싶다면,
[https://livesql.oracle.com/apex/livesql/file/content_GV8MU6SITA2V3VYI179FAJUCY.html](https://livesql.oracle.com/apex/livesql/file/content_GV8MU6SITA2V3VYI179FAJUCY.html)로 접속,
RUN SCRIPT 버튼을 눌러주면 내 계정에서 사용이 가능함.

[https://livesql.oracle.com/apex/f?p=590:49:::NO:::](https://livesql.oracle.com/apex/f?p=590:49:::NO:::)로 접속 하면 그 외 샘플 데이터와 학습 자료들이 있음.
**단점**이라면 영어라는것..?

