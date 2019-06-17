#### Database & SQL Basic 8

##### 복습

- 순위관련 함수

  - rank() over (partition by 컬럼 order by 컬럼 rows|range  unbounded preceding|between current row and unbounded following | n preceding |n following |) 

  - dense_rank()

  - row_number()

    

- 집계관련 window 함수

  - sum(), min(), max(), avg(), count()

- 행순서 관련 함수

  - first_value(), last_value(), lag(컬럼, n, null대체값)
    lead(컬럼, n, null 대체값)

- DML

  - 새 데이터 추가
    - insert into 테이블명 (컬럼명 리스트) 
    - values (컬럼명 리스트의 순서와 타입에 맞는 값 리스트);
    - insert into 테이블명  values (테이블에 선언된 컬럼순서대로 모든 값);
    - values절에 null, default, 단일행함수 등 사용가능
      insert into 테이블명 (컬럼명 리스트) subquery; --컬럼명 리스트는 subquery의 컬럼순서 , 개수, 타입과 일치해야함
  - 컬럼 값 변경
    - update 테이블명 set 컬럼명=변경할 값 [, 컬럼명=변경할 값,...];
    - update 테이블명 set 컬럼명=변경할 값 [, 컬럼명=변경할 값,...] where 조건;
    - update 테이블명 set 컬럼명=(subquery) [, 컬럼명=변경할 값,...] where subquery;
    - update 오류 - 컬럼타입 불일치, 컬럼크기 불일치, 제약조건 오류
    - 변경할 값에 null, default, 단일행함수 등 사용가능
  - 행 삭제
    - delete from 테이블명; - 모든 행 삭제
    - delete 테이블명; - oracle에서는 from 생략 가능
    - delete from 테이블명 where 조건 ; --- 조건을 만족하는 행만 삭제
    - delete from 테이블명 where 컬럼연산자 (subquery);
    - 참조무결성제약조건 오류 : 참조하는 자식 레코드가 존재하면 부모 레코드는 삭제할 수 없음
      - 예) 부서테이블의 레코드를 삭제하려면 소속 사원이 없는 부서정보 레코드만 삭제 가능합니다.
  - merge
    - merge into 대상 테이블 t
    - using 소스테이블 s
    - on t(s.pk컬럼 = t.pk컬럼)
    - when matched then update set t.컬럼=s 컬럼..... 
    - delete.where 조건
    - when not then insert (t.컬럼리스트)
    - value (s컬럼리스트);

- TCL(Transaction Control Language)

  - Transaction - unit of work, all or nothing ACID
    - 원자성, 일관성, 격리성, 영속성
  - DB에서 Transaction 단위 - 하나 이상의 DML, 하나의 DDL, 하나의 DCL 
    - auto commit을 함 
      - 하나 이상의 DML로 구성된 트랜잭션은 명시적으로 commit, rollback 해야함
      - DCL, DDL - auto commit
    - 트랜잭션 수행중에 DB 연결된 세션이 정상 종료 될 경우(exit:) - commit
    - 트랜잭션 수행중에 DB 연결된 세션이 비정상 종료 될 경우 - rollback
      - savepoint 식별자; , rollback to savepoint 식별자;

- 읽기 일관성 

  -  변경중인 user는 자신이 변경중인 값이 조회되고, 변경중이지 않는 user들은 DB에 이전에 commit되서 저장된 값을 조회함
  - Lock과 undo data를 이용해서 읽기 일관성 보장함
  - undo data는 트랜잭션을 rollback을 하면 변경전값을 undo segment로부터 restore(복원)함.

- 데이터베이스의 객체

  - table 
    - 구조, 물리적 data (Record+column)
    - heap, partition, IOT, cluster
  - view 
    - table에 대해서 select로 정의된 table의 window역할
    - 보안, 간결한 select문 사용을 위해서 base가 되는 table이나 view가 있어야 합니다.
      - 예외) MeterializedView - 성능향상이 목적인 물리적 data를 가지는 View
  - index 
    - 테이블의 컬럼에 생성
      - where절에 검색조건으로 사용되는 컬럼, join 컬럼, order by 절의 컬럼
      - 내부적으로 oracle server가 select 수행시 사용 b*tree구조로 저장
  - sequence
    - 순차적으로 숫자값이 저장되어야 하는 컬럼(주문번호, 게시판의 최소값, 최대값, 증감값 설정함)
  - Synonym(동의어) - schema명, 객체@dblink명과 같은 객체 이름을 간결하게 사용하기 위한 동의어.

- 테이블 생성

  - create table 테이블명 (컬럼명 컬럼타입(크기) 제약조건|default 기본값,)
  - [tablespace 저장소명 storage...];
  - 테이블 생성을 위해 필요한 권한 - create table 권한, tablespace에 대한 quota가 할당되어 있어야함

- 테이블 명, 컬럼명 이름규칙

  - 대소문자 구별 안함 - Data Dictionary에는 대문자로 저장됨
  - 첫 문자로 영문자, _, $, # 허용
  - 두번째 문자부터 숫자 허용
  - 키워드 허용 X
  - 동일 schema 내에서 같은 이름의 객체 X
  - 길이제한 30자 (데이터베이스이름 길이 제한 8자)

- schema - 서로 연관된 객체들을 그룹핑, 오라클에서는 user 명을 schema 명으로 사용함

  - user 소유의 객체들을 그룹핑해서 다른 user 소유의 객체들을 구별하는 namespace역할을 하면서 동일한 이름의 객체를 다른 schama에서 사용가능

- 컬럼타입

  - char
  - varchar2
  - number
  - datge
  - timestamp
  - timestamp with timezon
  - interval year to month
  - interval day to second
  - Bfile
  - BLOB (Long Raw)
  - CLOB(Long)
  - RAW
  - rowid - 행 주소 (objectid+fileid+blockid+행순서번호)

  

  - create table 테이블명 (컬럼명 리스트)

```sql
as select ~
	from ~
	[where ~]
	..... : 
select 절의 컬럼 리스트와 create table 절에 선언된 컬럼명 리스트의 순서

#테이블 구조 복제
create table 테이블명 
as select ~
	from ~
	where 1=2; --false조건
```



##### sql

- 제약조건(constraint)
  - DML 수행시 컬럼값의 허용 또는 제한규칙
  - primary key 
    - unique + not null
  - not null 
    - null 허용X, 컬럼레벨에서만 제약조건 선언 가능
  - unique
    - 중복값을 허용하지 않음,. oracle에서는 null은 unique 값으로 취급해서 여러개 허용
  - check 
    - 특정값의 허용 범위

```sql
create table emp2 (
empno  number(4),
ename varchar2(15) constraint 이름 not null,  ---컬럼 레벨
hiredate date,
job  varchar2(15),
sal  number(8, 2),
constraint emp2_pk  primary key (empno, ename) ---테이블 레벨
);

```

- 컬럼에 index가 자동 생성되는 제약조건 - primary key, unique key
  - 제약조건 메타 정보 조회 
    - user_constraints, all_constraints, dba_constraints
  - 테이블의 메타 정보 죄회
    - user_tables(tab), all_tables, dba_tables
  - 컬럼 메타 정보 조회
    - user_tab_columns
  - 인덱스 메타 정보 조회
    - user_indexes, user_ind_columns
- foreign key
  - 제약조건이 참조하는 부모 컬럼에는 primary key 또는 unique key 제약조건이 선언되어 있어야 함.

- PK와 UK에 index 자동 생성 목적 - 적합성 체크, 중복값 체크를 빠르게 수행. 

  

- index 생성에 적합한 조건

  - where 조건에 사용되는 컬럼
  - join 컬럼
  - order by 컬럼
  - 컬럼중에서 distinct value(선택도)값이 많아야 합니다.

  - where 절의 조건 = 연산조건의 결과 행이 5% 이내
    - 만약 10%를 초과하면 손익분기점으로 table full scan이 더 유리함! 
  - 자주 update되는 컬럼은 인덱스 생성하면 성능이 저하
  - 한마디로 거의 update가 발생하지 않는 컬럼에만 적합
  - 4~6개의 block 이상에 데이터가 저장된 테이블 

- 인덱스의 종류

  - 단일컬럼인덱스
  - 복합컬럼인덱스
  - unique 인덱스
  - non-unique 인덱스
  - function-based 인덱스 (컬럼값의 내림차순으로 생성, 컬럼표현식)
  - bitmap 인덱스
    - OLTP - B*Tree 인덱스
      - 소량drop , 빠른 검색
    - OLAP  - 분석 추리 - 빠른 and / or 수행시 유리
    - DW 
    - DSS
  - create index 인덱스명 on 테이블(컬럼);
  - alter index  인덱스명 on 테이블 (컬럼 desc);
  - drop index 인덱스명;

  

  

  - alter table 테이블명 modify (컬럼 컬럼타입(크기));

    - 컬럼 타입 변경 시 컬럼값이 존재하더라도 char(5) -> varchar2(10) 변경은 가능
    - 컬럼 타입 변깅 시 호환되지 않는 컬럼타입으로 변경 시, 컬럼값을 null로 변경한 후에 컬럼타입을 변경가능.
    - 컬럼 크기를 변경 시, 크기 증가는 항상 가능하지만, 컬럼값이 존재 시, 컬럼 크기를 줄이려면 현재 저장되어있는 컬럼값의 최대 길이보다 작게 줄일 수 없음
    - not null 제약조건 추가

    

    

    - alter table 테이블명 add constraint~;

    - alter table 테이블명 drop constraint~;. 

    - alter table 테이블명 add(컬럼 컬럼타입(크기), 컬럼 컬럼타입(크기).....)

    - alter table 테이블명 drop(컬럼 컬럼타입(크기), 컬럼 컬럼타입(크기).....)

    - alter table 테이블명 drop column 컬럼명;

    - alter table 테이블명 rename column old명 to new명;

    - alter table 테이블명 enable constraint~; (disable을 시킨 후에 추가한 것을 제거해야 enable 가능!)

    - alter table 테이블명 disable constraint~;

      

    - drop table 테이블명; 

      -  테이블이름이 rename되어 recyclebin에 저장됨(저장 공간 부족 시 서버에서 제거함) 

    - drop table 테이블명;

      - recyclebin을 bypass하고 물리적으로 완전 삭제됨.

    - truncate table 테이블명 [reuse storage]; - 구조만 남겨두고, data는 완전 삭제(recyclebin에도 undo data도 생성하지 않음)

    - drop table ~ : table의 meta 정보, data, 컬럼의 제약조건, 컬럼의 index도 함께 삭제!

      

      

  - view

    - simple view

      -  하나의 대상 테이블로부터 view 생성, not null 제약조건이 선언된 컬럼은 모두 포함, 컬럼표현식X, group by X, 그룹함수 X, rowid X, rownum 컬럼x, DML이 가능한 View (간접적 table access DML 수행됨)

    - complex view 

      - 하나 이상의 테이블에 대한 select 문으로 정의, 컬럼표현식 , group by  , 그룹함수  , 조인, rowid  , rownum 컬럼 등 포함된 경우, DML이 불가능한 View

    - create view 권한이 있어야 함.

      

  - view 객체 삭제는 테이블에 영향을 주지 않고 메타 정보만 data dictionary로부터 제거됨

    - check option(check 제약조건), read only,(select만 가능 - DML은 가능 하지 않음)

    

  - sequence

    - 특정 규칙에 맞는 연속 숫자를 생성하는 객체임.
      - 시퀀스 객체를 생성하면 자동으로 시퀀스의 내장 컬럼 currval, nextval을 생성합니다.
        - nextval을 한 후에 currval을 해야함.

  ```sql
  --alter sequence 시퀀스명
  increment by ~
  maxvalue ~
  minvalue ~
  cycle ~
  cache~;
  
  drop sequence 시퀀스명; -- 메타 정보만 data dictionary로 부터 삭제 됨.
  ```
  - Synonym
    - 테이블, 뷰, 시퀸스 등 객체 이름 대신 사용할 수 있는 다른 이름을 부여하는 객체임.
      - create public synonym 동의어이름 from 사용자 객체이름;
    - 삭제는 drop synonym 이름 으로 함

- 사용자 관리

```sql
conn hr/oracle
select *
from emp; -->error , select * from hr.emp;를 수행함

select *
from scott.emp;  --->권한없어서 오류



conn / as sysdba
create user kim
identified by 1234
password expire;

conn kim/1234 

--alter user kim identified by 새비밀번호;
--password 명령어로 비밀번호 변경

conn kim/oracle
-- create session 권한 (DB connetion권한) 없다고 오류 

conn / as sysdba
grant create session to kim;


conn kim/oracle
create table test (name varchar2(10));   --error

select user from dual;


#dual -----소유자? 
select owner, table_name
from all_tables
where table_name='DUAL';   --sys

public으로 dual 테이블에 대한 select권한을 줌

desc dual  -- ?  dummy컬럼 존재
select * from dual;   ---? dummy컬럼값은 x

-- dual의 목적....from절이 필수이므로 단순 계산결과, 함수 결과를 확인할때

-- 권한
-- 시스템 권한 - DB에서 특정 SQL을 수행할 수 있는 권한
-- 객체 권한 - EX) 예) table에는 insert, update, select, alter, delete등을 수행 권한
               -- view에는 select, drop , insert, update, delete
                --sequence는 select, alter, drop
          	-- 객체의 소유자, DBA
--객체 권한은 직접 권한을 준 유저가 회수를 가능
-- 객체 권한은 cascade로 회수가 됌. (a가 b한테 주고 b가 c한테 줬다고 했을 때, a가 b에게 뺏으면 c도 같이 뺏김)

-- 권한 관리를 쉽게 하려면 
-- 직무별, 업무별로 필요한 권한을 그룹핑 -Role
-- Role을 생성할 수 있는 권한은 DBA
-- 1. create role 롤이름;
-- 2. grant 시스템권한, 객체 권한 to를 이름;
-- 3. grant 롤이름 to 사용자|롤이름|public;

-- revoke 롤 이름 from 사용자|롤이름|public

--user_role_privs
-- drop role 롤이름 
-- Role의 또 하나의 장점은 동적 권한 관리 가능

```

