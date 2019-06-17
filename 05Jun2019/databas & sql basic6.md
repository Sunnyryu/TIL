DataBase & SQL

#### 복습

- subquery - select문 내부에 정의된 select문(inner query, nested query)
- outer query, main query
- 2번 이상 select를 수행해서 결과 집합을 생성해야 할때 ..하나의 select문으로 정의해서 실행시킴
- single row subquery - scalar subquery
- multiple row subquery - mutiple column subquery
- subquery가 main query보다 먼저 수행하고, 1번 수행
- co-related subquery(상관관계 subquery) - subquery가 main query의 컬럼을 참조해서, main query의 행수만큼 subquery 반복적으로 수행하는 Query

- subquery가 올 수 있는 위치 
  - select절
  - from절  ---inline view
  - where절  --연산자 오른쪽 (subquery)
  - having절  --연산자 오른쪽 (subquery)
  - order by절

- subquery를 where절이나 having절에 정의할때 single row subquery는 single row operator(>, >=, <, <=, !=, <>) 함께 사용
- multiple row subquery는 multiple row operator (in, any>, any<, all<, all>)

- subquery에는 모든 select절, 함수등 제약없이 사용 가능하지만, order by절은 from절의 inline view에서만 허용됨

- rownum -결과행에 순차적인 번호를 발행 내장 컬럼

- rownum은 order by 전에 발생되므로, order by 후에 rownum으로 순차적인 번호를 발행하려면 subquery를 사용합니다.

- co-related subquery(상관관계 subquery)

  ```sql
   select~~
   from  table1 a
   where column 연산자 (select ~
                        from table2
                        where a.column = column2)
  ```

- co-related subquery에서 존재 유무를 체크해주는 연산자 - exists, not exists

```sql
-- 긴 query문에서 반복적으로 사용하는 subquery를 먼저 정의해서 재사용하려면
with 
별칭 as (subquery),
별칭 as (subquery),
별칭 as (subquery),
....
별칭 as (subquery)
select ~
from ~
where ~
```

- 집합연산자(set operator)
- 서로 다른 select의 결과를 단일 결과집합으로 만들기 위해 사용하는 연산자
  - 합집합 : union, union all
    - 각 select의 중복된 행을 제외시킴(union)
      - 첫 번째 컬럼값으로 정렬하여 비교함.(append 방식)
    - 각 select의 중복된 행을 포함시킴(union) 
  - 교집합 : intersect
    - 각 select의 결과 행에서 중복된 것만 가져옴
      - 첫 번째 값으로 정렬하여 비교함
  - 차집합 : minus
    - 첫 번째 select의 결과에만 속한 행을 선택하기 위한 비교를 방식 

```sql
select ~
from ~
[where ~]
[group by ~]
[having ~]
union, union all, intersect, minus
select ~
from ~
[where ~]
[group by ~]
[having ~]
[order by ~]
-- 각 select문에서 컬럼개수와 컬럼타입이 일치해야함.
-- 결과는 첫번째 컬럼값을 기준으로 정렬된 기준으로 리턴되므로 다른 컬럼으로 정렬하려면 order by절에는 마지막 select 절에만 허용됨.
```

- rollup
- cube
- grouping sets
  - 필요한 것을 넣을 때 넣은 것만 나열하는 것(효율성이 떨어짐.)



#### 데이터 언어

- 새로운 데이터를 추가하려면 대상 테이블에 insert 권한 또는 테이블의 소유자
- insert into 테이블명  (컬럼명, 컬럼명,...) 
- values (컬럼리스트의 순서대로 값...);
- ※새로 추가되는 행의 데이터로 일부 컬럼값만 정의할 경우, 필수 컬럼은 반드시 포함되어야 합니다.
- insert into 테이블명  values (테이블에 정의된 컬럼 순서대로 모든 값이 선언);

```sql
insert into dept (dname, loc)
values ('IT', 'Seoul');  -->error 

--alter table dept add constriant primary key (deptno);

insert into dept (deptno, dname )
values (50, 'IT' );
select * from dept; 

insert into dept 
values (55, 'ERP', null);
select * from dept; -- 가능


insert into dept 
values (150, 'HR', null);  --error 컬럼size초과


insert into dept 
values (50, 'HR', null); --error, deptno(PK)에 중복값 ...


insert into emp (empno, ename, deptno)
values (9000, 'Kim', 70); -----error, deptno(FK)의 참조컬럼에 70번데이터가 존재하지 않으므로, 참조 무결성 제약조건 오류



insert into emp (empno, ename, deptno, hiredate)
values (9000, 'Kim', 50, sysdate); -- ?

insert into emp (empno, ename, deptno, hiredate)
values (9001, 'Lee', 50, '19년3월2일');  -- eror 발생
insert into emp (empno, ename, deptno, hiredate)
values (9001, 'Lee', 50, '19/03/02'); --- 에러 발생 시에 to_date를 사용한다.

또는

insert into emp (empno, ename, deptno, hiredate)
values (9001, 'Lee', 50, to_date('19/03/02')); 

create table emp10 
as select * 
   from emp
   where 1=2; ---테이블 구조만 복제, CTAS

desc emp10
select * from emp10;

  
insert into emp10
select * from emp where deptno = 10;
--values 절 대신 subquery를 선언하면 subquery의 결과 행수만큼 추가됨.

select * from emp10;


insert into emp10 (empno, ename, deptno, sal)
select empno, job, hiredate, mgr
from emp where deptno = 20; 
--subquery에서 insert에 선언된 컬럼 개수나 타입과 일치하지 않으면 error 발생


# 테이블에 이미 존재하는 행의 데이터를 수정할때 컬럼단위로 수정합니다.
update 테이블명
set 컬럼명=new컬럼값 [, 컬럼명=new컬럼값, ...];  --테이블의 모든 데이터의 변경컬럼값을 단일 값으로 변경함

select empno, ename, deptno, sal from emp10;
update emp10
set sal = 1;
select empno, ename, deptno, sal from emp10;
rollback;
select empno, ename, deptno, sal from emp10;



update 테이블명
set 컬럼명=new컬럼값 [, 컬럼명=new컬럼값, ...]
where 조건;

select empno, ename, deptno, sal 
from emp;

update emp 
set sal = 1
where deptno = 30;

select empno, ename, deptno, sal 
from emp;

rollback;

select empno, ename, deptno, sal 
from emp;



update dept
set deptno = 40
where dname  = 'IT';  --?error, 중복값

update emp
set deptno = 60
where empno = 7788;   --?error, 참조무결성제약조건 오류


문> SMITH사원의 급여를 KING사원의 급여와 동일하도록 변경하세요
--update의 set절 subquery
--update의 where절 subquery
update emp
set sal = (select sal from emp where ename = 'KING')
where ename = 'SMITH';

rollback;
ex> KING사원과 동일한 부서에 근무하는 KING을 제외한 다른 사원의 급여를
20%인상 수정함
update emp
set sal = sal*1.2
where deptno = (select deptno from emp where ename ='KING')
and ename <> 'KING'

```

```sql
select * from customer;

insert into customer (custid, custname)
values (990301, 'Kim');

select * from customer;  
---생략된 point컬럼값은 기본값 1000자동 입력됨?

update customer
set point = null;

select * from customer;  

update customer
set point = default;

select * from customer;  


테이블이 이미 저장되어 있는 레코드를 삭제하려면
delete from 테이블명 ;  ---전체 행 삭제
delete table명 -- 오라클에선 from이 생략 가능
delete from 테이블명 where 조건 ; ---조건을 만족하는 행만 삭제
delete from 테이블명 where 컬럼 연산자 (subquery)

select * from emp;
delete from emp;
select * from emp; 
rollback;


delete from emp where deptno = 30;
select * from emp; 

rollback;
select * from emp;

delete from dept; ---? 참조하는 자식 레코드가 존재하면 부모 레코드 삭제 불가 (참조 무결성 제약조건 오류)

delete from dept where deptno = 55; -- 55번 부서번호 삭제..

-- ex)  ADAMS 사원과 동일한 직무를 담당하는 사원 삭제 (ADAMS 사원은 제외)
delete from emp
where job = (select job from emp where ename = 'ADAMS')
and ename <> 'ADAMS';
```

- merge
  - 변환 작업을 하고 로딩을 하는 구문들이 있는데,  머지는 이관작업(ETF) 시에 사용함
    - update - delete를 한 번에 할 수 있어, rollback 1번만으로도 취소 가능

```sql
merge into 대상테이블 t(aliss) using 소스테이블 s on t.pk컬럼 = s.pk컬럼 when matched then update set t.컬럼=s.컬럼.... [delete.where 조건] when not match then insert (t.컬럼리스트) values (s.컬럼리스트);
```

- Trasaction - Unit of Work (분리되어 수행될 수 있는 작업단위)
- ACID - 원자성, 일관성, 격리성, 영속성
- DB 관점의 Transaction
  - Select는 포함되지 않으며, 
  - 변경(DML, DDL, DCL)이 포함되면
- Transaction 단위
  - 1개이상의 DML들로 구성 - 명시적 commit, rollback
  - 1개의 DDL - auto commit;
  - 1개의 DCL - auto commit;;

```sql
-- 수행중인 DML 트랜잭션의 세션이 비정상종료하면 oracle server는 rollback
-- 수행중인 DML 트랜잭션의 세션을 정상종료(exit:)하면 oracle Server는 commit 
```

- 읽기 일관성 : select하는 user들이 변경중인 user 작업이 종료될 때까지 기다리지 않아도 되고
- 변경 작업하려는 user들은 select하는 user들이 검색을 종료할때까지 기다리지 않고
- 변경 작업중인 user들은 변경중인 값을 조회 결과로 볼 수 있고,
- 변경 작업중인 user들은 db에 저장된(commit된) 데이터 값을 조회 결과로 볼 수 있도록...commit됨.

- 오라클 서버는 읽기 일관성을 위해서 Lock, undo segment등을 지원함.

```sql
create table test (num number(2));
insert into test values (1):
insert into test values (2):
savepoint a;
insert into test values (3):
insert into test values (4):
savepoint b;
insert into test values (5):
insert into test values (6):
select * from test;
-- 만약 그냥 롤백하면 전체가 다 취소됨.
-- rollback to savepoint b;라면 1,2,3,4는 남게됨.
-- rolback to savepoint a;라면 1,2만 남게됨.
-- 필요한 부분만 남기고 commit 해줍니다.
```

- data base의 대표적인 개체
  - Table: row와 column으로 구성됨
  - 실제 물리적으로 저장된 파일의 데이터를 가짐.
    -  테이블이 여러가지 종류가 있는데, Heap Table, Index 구조, partition
  - view
    - 테이블과 유사함, rowdata와 columndate를 보여주는데, 테이블을 보여주는 window 역할
    - 물리적인 데이터가 없음, 논리적인 테이블이라고 부름.
      - 예외가 있는데 materialize view가 있음
        - select 문으로 정리함
    - 뷰를 사용하는 목적
      - 원본인 테이블에 민감한 요소가 들어가있는데, 수정하기 위한 도구가 필요함.
      - 그런데  보안상을 위해 일부분만 넣어서 보여주는 것을 뷰라고 이해하면 됌.
      - 자주 사용하는 select 문을 뷰에 넣어 view로 나타내면 복잡한 쿼리 문을 간결하게 사용하기 위함.
  - 테이블 생성하려면 create table 시스템 권한이 있어야 합니다.
  - tablespace (data container)저장소에 quota가 할당되어 있어야 합니다.
  - table 또는 컬럼 이름 규칙
    - table 또는 컬럼 이름 규칙 :
    - 영문자 또는 _, $, #로 시작
    - 두번째 문자부터 숫자 허용
    - 키워드 안됨
    - schema내에서 중복된 이름 사용 불가
      - schema - 서로 연관된 table, index등의 객체를 그룹핑하는 논리적 개념
      - 객체 명을 재사용할 수 있는 namespace역할을 합니다.
      -  오라클은 user명을 schema명으로 사용합니다.
    - 길이 제한 30자
    - DB이름 길이 제한 8자
    - 컬럼타입 :
    - char : 고정길이 문자열 ~ 2000byte
    - varchar2 가변길이 문자열 ~4000byte
    - number(p, s)
    - date  세기,년,월,일,시,분,초 까지 저장
    - timestamp - date타입 확장 1/10^9 초까지 저장
    - timestamp with timezone
    - interval year to month
    - interval day to second
    - rowid
    - CLOB(character large object) ~4G (giga)
    - raw - binary 형식의 값 저장 예)지문, 증명사진 ~2000byte
    - BLOB(binary large object) ~4G
    - BFILE - read only 가능한 file을 DB외부에 운영체제의 폴더에 저장, TX처리 불가능

```sql
desc user_tables
select table_name, tablespace_name from user_tables;

create table 테이블명(
컬럼명 컬럼타입(size),
컬럼명 컬럼타입(size)[default 값],
컬럼명 컬럼타입(size)[제약조건],
........
[제약조건]
 )
[............];

CTAS이용해서 테이블 구조만 복제, 테이블 구조+데이터 복제 가능

create table 테이블이름
as
  (subquery);

create table emp20
as select empno, ename, deptno, sal*12
   from emp
   where deptno = 20; ---error
 
 create table emp20
as select empno, ename, deptno, sal*12 salary
   from emp
   where deptno = 20;
   desc cmp20
   select * from emp20;
   
   drop table emp20 purge;


create table emp20 (empid, name, deptid, salary)
as select empno, ename, deptno, sal*12  
   from emp
   where deptno = 20;
      desc cmp20
   select * from emp20;
   
-- 기존에는 drop table ooo;
-- data -> undo 생성없이 물리적 삭제, 구조 삭제, 복수하려면 매우 어려움
-- 현재 버전부터는 log Recycle bin - 휴지통을 조회하여 복원가능(Rename 된 이름)
-- purge를 추가하면 휴지통을 안거치고 삭제함.

create table copy_dept
as select * from dept;
desc copy_dept
select * from copy_dept;

drop table copy_dept;
desc copy_dept
select * from copy_dept;
select tname from tab;  ---BIN$~~~~~~~이름의 테이블
select * from user_recyclebins;
select * from  recyclebin ;
select * from "BIN$x1Y==$0";

flashback table copy_dept to before drop; -- 복구!
select * from  recyclebin ;
select tname from tab;
desc copy_dept
select * from copy_dept;

제약조건 constraint  table의 DML 수행시 규칙
Primary key
not null
Unique key
Foreign key
check

create table userinto
(userid varchar2(10) not null, username varchar2(15) constraint userinto__nn not null, age number(30));
desc userinfo
insert into userinto(username, age)
values('테스터1', 20)-- 에러

select * from userinfo;

select constraint_name, constraint_type
from user_constraints
where table_name = 'USERINFO';

alter table userinfo disable constraint userinfo_nn; -- 비활성화 시킴.

insert into userinfo  (userid, age)
values ( 'tester2', 30); 

select * from userinfo;

drop table userinfo ;
select * from userinfo;
desc userinfo

select constraint_name, constraint_type
from user_constraints
where table_name = 'USERINFO'; 

select * from recyclebin;
flashback table userinfo to before drop;

select constraint_name, constraint_type
from user_constraints
where table_name = 'USERINFO'; -


drop table userinfo purge;

-- ---unique 제약조건 ----
create table userinfo 
(userid  varchar2(10)  constraint userinfo_uk  unique,
 username  varchar2(15)  ,
 age  number(30)
);

desc userinfo
insert into userinfo 
values ('tester1', '테스터1', 20);

insert into userinfo  (username, age)
values ( '테스터2', 25);   

insert into userinfo  (username, age)
values ( '테스터3', 30);

select * from userinfo;

select constraint_name, constraint_type
from user_constraints
where table_name = 'USERINFO'

select index_name, uniqueness
from user_indexs
where table_name = 'USERINFO';

alter table userinfo disable constraint userinfo_uk; -- 비활성화 시킴
select index_name, uniqueness
from user_indexs
where table_name = 'USERINFO'; -- 삭제됨

alter table userinfo enable constraint userinfo_uk;
-- 활성화 시킴
select index_name, uniqueness
from user_indexs
where table_name = 'USERINFO'; -- 다시 복구함.
drop table userinfo purge;

-- ----------primary key 제약조건 -------------
--primary key = not null+unique
-- 다른 제약조건은 하나의 테이블에 여러개 선언가능합니다만,
-- primary key 제약조건은 하나만 선언 가능합니다.

create table userinfo 
(userid  varchar2(10)  constraint userinfo_pk primary key,
 username  varchar2(15)  ,
 age  number(30)
);

desc userinfo
insert into userinfo 
values ('tester1', '테스터1', 20);

insert into userinfo  (username, age)
values ( '테스터2', 25);    -- null은 안됨

insert into userinfo  (username, age)
values ( '테스터3', 30);    ---null은 안됨

insert into userinfo 
values ('tester1', '테스터5', 35); ---error tester1이 이미 있음.

select * from userinfo;

select constraint_name, constraint_type
from user_constraints
where table_name = 'USERINFO';

select index_name, uniqueness
from user_indexes
where table_name = 'USERINFO';
제약조건 : check  ***********************************************
create table userinfo(
userid  varchar2(10),
username  varchar2(15),
gender   char(1) constraint userinfo_ck  check (gender in ('F', 'M')),
age  number(2) check (age > 0 and age < 100)
);

select constraint_name, constraint_type, search_condition
from user_constraints
where table_name='USERINFO';

insert into userinfo  values ('a001', 'an', 'f', 20);  --error f가 소문자임
insert into userinfo  values ('a001', 'an', 'w', 20); --error 잘못된 문자
insert into userinfo  values ('a001', 'an', null, 20);   -- 가능
insert into userinfo  values ('a002', 'choi', 'M', 0); --error 0보다 커야함
insert into userinfo  values ('a002', 'choi', 'M', 100); --error 100보다 작아야함
insert into userinfo  values ('a002', 'choi', 'M', 25);  -- 가능

drop table user_info purge;


```





