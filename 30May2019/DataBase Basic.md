## DataBase & SQL

#### DataBase

- DataBase 전에는 *파일 시스템*을 사용함.
  - 파일은 중복이 가능해서 일관성이 결여되며, 통합하기가 불편하고 어플리케이션에 종속되다보니,  프로그램의 독립성 유지가 불가능 하며, 개발 생산성이 나쁘다.

- 데이터 베이스는 특정 기업이나 조직 또는 개인이 필요에 의해 논리적으로 연관된 데이터를 모아 일정한 형태로 저장해 놓은것
- DBMS(Database Management System)
  - DBMS를 이용하여 데이터 입력, 수정, 삭제 등의 기능이 제공됨.
- *DBMS의 장점*
  - DBMS를 이용하여 데이터 공유하기 때문에 중복가능성이 낮음
  - 중복 제거로 데이터 일관성 유지 !
  - 데이터 정의와 프로그램 독립성 유지 가능!
  - 데이터 복구, 보안, 동시성제어, 데이터 관리 기능을 수행함
  - 짧은 시간에 큰 프로그램 개발 가능
  - 데이터 무결성 유지 가능
- DB의 특징
  - 통합된 데이터, 저장된 데이터, 운영데이터, 공용데이터, 실시간 접근성, 지속적인 변화, 내용에 따른 참조
    - 통합된 데이터 : 데이터의 중복을 최소화하여 중복으로 인한 데이터 불일치 현상 제거
    - 저장된 데이터 : 디스크, 테이프 같은 컴퓨터 저장장치에 저장된 데이터
    - 운영 데이터 : 업무를 위한 검색을 할 목적으로 저장된 데이터
    - 공용 데이터 : 동시 공유
- 데이터베이스 사용자 그룹
  - 일반사용자, 응용프로그래머, SQL 사용자, DBA

- DBMS는 데이터베이스를 구성하는 프로그램과 메모리로 되어있음.
- 데이터 베이스 계층형 DBMS
  - 계층 구조상에서의 참조관계가 1:M의 관계임
  - 데이터에 대해서 기본개념은 레코드(ROW)임	
    - Ex) 학번, 이름, 점수 등 레코드로 저장함
    - 참조관계를 하려면 물리적인 포인터가 있어야함
    - 단점이 관리가 어렵다.(참조된 것을 삭제하면 포인터들을 다 일일이 삭제를 해야함)

- 그물망형 DBMS

  - 망형은 M : M으로 참조가 가능함.
    - 그렇지만 물리적 포인터는 개선되지 않음!

- 수학 관계 대수

  - ex) 학생도 이차원으로 구조로 되어있고 학생이라면 ... 교수, 과목에 대한 것도 이차원으로 구조로 표현
  - 과목에 대해서 , 교수에 대해서 여러 data가 있고 유일한 레코드를 식별하기 위한 식별키가 있어야함.
    - 부모의 존재하는 속성값만 가질 수 있고 부모에 존재하지않은 속성값은 변경하거나 삭제할 수 없음

- 수학 관계 대수를 이용하여 RDBMS가 나옴

- RDBMS

  - 이차원 구조로 되어있는 것을 테이블이라는 구조로 사용

  - Entity를 테이블로 설계함

  - 학생에서 학번, 과목에서 교과목 이라는 것을 하나의 레코드를 쓸 수 있는 키를 프라이머리 키라고 함.

    - 프라이머리 키 not null + unique

    - 과목코드라는 속성이 있다고 하면 과목이라는 것을 참조하지만 학생의 참조는 아니지만

      -  외래키라고 용어로 사용함

        > 1980년 대 이후에 객체지향을 활용한 프로그래밍이 활발해지고 1990년대에 객체지향 프로그래밍을 하면서 매칭이 안되는 문제점이 나타나는데 객체지향 프로그램을 쓰기 위해 객체지향 DBMS를 만들기 시작함...

  

- ORDBMS

  - RDBMS의 문제점을 해결하기 위해 만듬

  - 객체형을 지원하는 DBMS임.

  - 웹에서 발생하는 데이터들을 수용해야하고 볼륨이 커지게 되는데 한 개에 저장할 수 있는 시스템에 한계가 있다보니 문제가 발생함.

    - 해결하기 위해 여러 노드를 연결하여 저장하고 클러스터로 사용하지만 감당이 안됨..

    - NoSQL이나 다양한 것들이 등장하게 되었지만 RDBMS는 계속 사용함..

      > (스키마는 데이터 베이스 전체의 논리적 구조와 물리적 구조를 기술한것. )

- DBMS에서는 Table = Entity(READ 집합), Raw = Record = tuple(속성값 모음)
  - column = attribute (속성), primary key 속성 = Not Null+Unique
  - Foreign Key= 외래 키, SQL = Strucctured Quety Language)

#### SQL

- DML - DQL select검색/ Insert추가/Update수정/삭제Delete
- DDL - 명령(Create), 변경(Alter), 삭제(Drop)
- DCL는 인*증*을 거쳐야하며 *권한*을 주거나 회수할 수 있음
  - 권한을 줄떄는 Grant, 회수할 떄는 Revork
- RDBMS는 중점은 트랜잭션 처리
  - 트랜잭션은 분리되서 수행될 수 없는 단위(Unit of Work)
    - 원자성을 가져야함 (쪼갤 수 없음)
      - ex) 이체 중에 정전이 발생할 때, 돈이 인출이 안된다면 .. 큰일 나듯이..
    - 트랜잭션에는 Commit, rollback이 쓰임(TCL)
- SQL 실행전에 해야할 것

```
# sqlplus를 실행시키고 관리자 계정으로 접속해서 sample계정 비밀번호 설정하고, 잠긴 계정을 풉니다.
C:\Users\student>sqlplus / as sysdba

SQL*Plus: Release 11.2.0.1.0 Production on 목 5월 30 10:20:16 2019

Copyright (c) 1982, 2010, Oracle.  All rights reserved.


다음에 접속됨:
Oracle Database 11g Enterprise Edition Release 11.2.0.1.0 - 64bit Pro
With the Partitioning, OLAP, Data Mining and Real Application Testing

SQL> select user from dual;

USER
------------------------------
SYS

SQL> alter user scott
    identified by oracle
     account unlock;

사용자가 변경되었습니다.

SQL> alter user hr
     identified by oracle
    account unlock;

사용자가 변경되었습니다.
```

- Select 하나에 엄청나게 복잡한 과정이 들어감
- Sql 처리에 사용되는 메모리가 있다. library cache

- 이전에 동일한 처리를 한 적이 있는지 체크. 있으면 바로 리턴

- Soft passing
  - Syntax Checking
  - library cache
  - 테이블 정보, 컬럼, 권한 등 checking
    - user table 컬럼 제약조건 = meta 정보, 시스템 카탈로그,data dictionary
    - semantic checking
    - optimize Checking
  - optimizer



