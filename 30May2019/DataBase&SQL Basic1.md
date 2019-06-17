## DataBase & SQL

#### DataBase

- DataBase는 user와 meta data로 저장됨..

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

  - 이차원 구조로 되어있는 것을 테이블(가장 기본적인 단위)이라는 구조로 사용

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

- DBMS에서는 Table = Entity(READ 집합),
  
  - Raw = Record = tuple(속성값 모음)
  - column = attribute (속성), primary key 속성 = Not Null+Unique
  - Foreign Key= 외래 키, SQL = Strucctured Quety Language)
  - 참조관계(parent 테이블의 PK를 참조하는 chid 테이블의 외래키를 설정)
  - null - 아직 값이 할당되지 않음을 의미, 0이 아니며 ""와 다르며
    - 산술 연산 , 비교연산, 논리연산의 결과가 모두 null임.

#### SQL

- 선언적 언어 결과, 기술

- DML - DQL 
  - select : 테이블에서 조건에 맞는 튜플을 검색, 데이터를 조회
  - Insert : 테이블에 새로운 튜플을 삽입, 데이터를 삽입
  - Update : 테이블에서 조건에 맞는 튜플의 내용을 변경, 데이터를 수정
  - Delete :테이블에서 조건에 맞는 튜플을 삭제, 데이터를 삭제
- DDL - 
  - Create : SCHEMA, DOMAIN, TABLE, VIEW, INDEX를 생성
  -  Alter : TABLE에 대한 정의를 변경하는 데 사용
  - Drop :  SCHEMA, DOMAIN, TABLE, VIEW, INDEX를 삭제
  - TRUNCATE : 구조를 제외하고 모든 데이터를 초기화시키는 역할
  - Rename : 테이블 이름을 변경할 때 사용함
  - comment도 있음
- DCL는 인*증*을 거쳐야하며 *권한*을 주거나 회수할 수 있음
  - 수행 권한을 줄떄는 Grant, 수행 권환 회수할 떄는 Revork
- RDBMS는 중점은 트랜잭션 처리
  - 트랜잭션은 분리되서 수행될 수 없는 단위(Unit of Work)
    - 원자성을 가져야함 (쪼갤 수 없음)
      - ex) 이체 중에 정전이 발생할 때, 돈이 인출이 안된다면 .. 큰일 나듯이..
    - 트랜잭션에는 Commit, rollback이 쓰임(TCL)
      - Commit : 명령에 의해 수행된 결과를 실제 물리적 디스크로 저장하고, 데이터베이스 조작 작업이 정상적으로 완료되었음을 관리자에게 알림
      - Rollback : 트랜잭션의 작업을 취소 및 복구하는 역할, 데이터베이스 조작 작업이 비정상적으로 종료되었을 때 원래의 상태로 복구
      - SavePoint : 현재 트랜잭션 내에 SAVEPOINT명의 저장지점을 설정한다.
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

```
SQL> conn hr/oracle

SQL> select * from employees

SQL> conn scott/oracle

SQL> select tname from tab; ---메타정보로 테이블 목록 확인

SQL> select * from emp;  --테이블의 모든 데이터 조회



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
  - optimizer(비용 선택(무료인 곳, 가장 빠른곳))

```sql
sqlplus 툴 - sql 실행, 결과 보여주는 환경 제공
sqlplus 툴 명령어 - 세미콜론(;) 없이 사용 가능, 명령어 축약  사용 가능
sql문은 명령어 축약 불가, 반드시 한 문장은 세미콜론(;) 으로 종료
sql 검색구문은 
select * | [distinct] colimn..... | expression [as] Alias
from 테이블명
[where 조건]
...
[order by 정렬기준 컬럼 asc, desc(생략시 asc)]
테이블 구조 확인 - desc
컬럼타입 :
char(1) ~2000byte
varchar2(1) ~4000byte
number타입 binary형식으로 정수, 실수
date 날짜를 7byte를 사용해서 수치값으로 저장 (__세기, __년도 __월 __일 __시 __분 __초)
number(p, s)
date
timestamp,
timestamp with timezone 
interval year to month
interval day to second
rowid
number - 산술연산
컬럼타입에 따른 연산 :
char/varchar2 - || 결합연산자
date - +- 정수, +- 1/24, date-date
where 절 연산자 :
in - 여러 값의 리스트에서 값들을 =로 비교, or
like - 문자로 패턴 비교  _, % 만능문자와 하께 사용합니다.
between - and - (범위 연산자 하한값 / 상한 값 순서로 해야함)
is null, is not null 비교
=,>, <=, >=, !=, <>
조건이 여러개 이면 논리연산자로 결합(우선 순위 : not, and, or)
ore\der by 컬럼;
order by 표현식;
order by 별칭;
order by 컬럼의 위치값;


select sysdate from dual; --시스템 현재 시간을 리턴하는 함수

--세션에 설정된 기본 날짜 출력 형식은  RR/MM/DD입니다.
SQL> select sysdate from dual;   

SYSDATE
--------
19/05/30

--세션의 날짜 출력 형식을 변경 
SQL> alter session set nls_date_format ='YYYY/MM/DD HH24:MI:SS';

세션이 변경되었습니다.

SQL> select sysdate from dual;

SYSDATE
-------------------
2019/05/30 11:23:08

SQL> exit;  --db disconnection, 세션 종료
 


--세션을 종료한 후에 다시 시작하면 세션의 기본 날짜 출력 형식으로 변경됩니다.

C:\Users\student>sqlplus scott/oracle

SQL> select sysdate from dual;   

SYSDATE
--------
19/05/30
```



```sql
meta정보가 저장된 oracle data dictionary view는 
user_tables - 특정 user 소유의 테이블 목록 확인
all_tables - 특정 user 소유 + 권한을 받은 테이블 목록 확인
dba_tables - DB의 모든 테이블 목록 확인 (DBA 권한으로만 확인 가능)

desc user_tables
select table_name from user_tables;  -user_tables의 별칭 tab
desc tab
select tname from tab;

select table_name from all_tables;
select table_name from dba_tables; --오류 발생

conn / as sysdba
select table_name from dba_tables;


conn scott/oracle

※sql문장의 키워드와 테이블명, 컬럼명등은 대소문자 구별 안합니다. 
※컬럼값은 대소문자 구별합니다.

SQL> host cls

--조회할 컬럼의 순서는 테이블에 정의된 컬럼순서에 맞추지 않다도 됩니다.
select ename, sal, job, deptno from emp; 

select deptno from emp;
select distinct deptno from emp; -- hashing방식 사용해서 중복값 제거

select deptno, distinct job from emp; --?error
--주석
select distinct deptno,  job from emp;


number타입 컬럼은 산술연산 :  +,-, *, /
char/varchar2 타입 컬럼은 문자열 결합 : ||
date 타입 컬럼 :  date±n, date-date, date±1/n


select sal+100, sal-100, sal*2, sal/100
from emp;

select sal, comm, (sal+comm)*2
from emp;

--데이터가 추가될때 입력되지 않는 컬럼값은 null입니다.
--null은 아직 값이 없다는 의미입니다. , 0도 아니고, ''도 아닙니다.
--null은 산술연산 수행 결과는 항상 null입니다.
--null을 포함하는 컬럼들은 null아닌 값으로 변환 후에 산술연산을 수행해야 합니다.
--모든 DBMS에서는 null아닌 값으로 변환해주는 내장 함수를 제공합니다.
--nvl(column, null일때리턴값)
--null은 비교연산, 논리연산 모두 null이 결과입니다.

select sal, comm, (sal+nvl(comm, 0))*2 as salary
from emp;

select sal, comm, (sal+nvl(comm, 0))*2 as "Salary"   --대소문자 구별
from emp;

select sal, comm, (sal+nvl(comm, 0))*2 "Total Salary"   --공백 포함 대소문자 구별
from emp;

※ 문자, 날짜 데이터는 반드시 ' '를 사용해서 표현, 처리
※ 날짜 데이터 세션에 설정된 포맷 형식하고 일치해야 합니다. ('RR/MM/DD')

select   ename||job
from emp;


select   ename|| ' works as ' ||job
from emp;

Quiz> 'A' 결과로 출력하려면?
select  '''A'''
from dual;

select  q'['A']'
from dual;

※ select~ from절이 필수절입니다.
※ 단순계산 결과, 함수 결과, 문자 데이터 출력등은 dual테이블을 사용합니다.
desc dual
select * from dual;

Quiz> select 10||10 from dual;  --?oracle server가 정수10을 문자열로 자동 형변환
Quiz> select '10'+'10' from dual; ---? 문자열10을 정수로 자동 형변환


select sysdate+1, sysdate-1
from dual;     --날짜와 산술연산하는 정수는 Number of Days입니다.

select sysdate-hiredate
from emp;     --기간이 리턴

select sysdate_hiredate
from emp;   --error

alter session set nls_date_format='YYYY-MM-DD HH24:MI:SS';
select sysdate, sysdate+1/24, sysdate+5/1440
from dual;
```









