#### Database & SQL Basic 9

##### 정리

- 테이블

  - 테이블 컬럼 추가 

    - alter table ~ add (컬럼 컬럼타입 [제약조건]);

  - 테이블 컬럼 삭제 

    - alter table ~ drop column 컬럼명;

    - alter ~ drop (컬럼,컬럼);

  - 테이블 컬럼 이름 변경 

    - alter table ~ rename column old to new;

  - 테이블 컬럼타입 또는 size 변경

    - alter table ~ modify (컬럼 컬럼타입(size ))

  - 제약조건을 컬럼추가

    - alter table ~ add constraint 이름 타입 

  - 컬럼에 정의되어 있는 제약조건 삭제 

    - alter table ~ drop constraint 이름;

  - 제약조건을 활성화, 비활성화 

    - alter table 명 ~ enable constraint 이름; / alter table ~ disable constraint 이름;

  - 테이블 삭제 

    - drop table ~ ;  또는 drop table ~ purge;
    - recyclebin으로부터 drop된 테이블 복원 : flashback table ~ to before drop;
    - drop table ~ : table의 meta 정보, data, 컬럼의 제약조건, 컬럼의 index도 함께 삭제!

  - 테이블 정리 

    - truncate table 테이블명 [reuse storage]; - 구조만 남겨두고, data는 완전 삭제(recyclebin에도 undo data도 생성하지 않음)

- 뷰

  - 논리적 테이블, table에 대한 window
  - Simple View(보안) / Complex View(간결한 sql)
  - Simple View
    - 하나의 대상 테이블로부터 view 생성, not null 제약조건이 선언된 컬럼은 모두 포함, 컬럼표현식X, group by X, 그룹함수 X, rowid X, rownum 컬럼x, DML이 가능한 View (간접적 table access DML 수행됨)
  - complex view 
    - 하나 이상의 테이블에 대한 select 문으로 정의, 컬럼표현식 , group by  , 그룹함수  , 조인, rowid  , rownum 컬럼 등 포함된 경우, DML이 불가능한 View
  - view 사용 목적
    - 보안, 간결한 sql 사용

  ```sql
  create [or replace ] [force|noforce] view 뷰이름
  as
     select ~
     from ~
     where ~
     group by ~
     having ~
     order by ~
     with check option - 체크 제약 조건 
     with read only - read only 제약조건
  ```

  - user_views, all_views, dba_vies - text컬럼 확인 가능
  - alter view 구문 x 
  - drop view 뷰이름 - 테이블에 영향을 주지 않음. 
  - 테이블 삭제하면 구조와 데이터 삭제, 제약조건, 인덱스
  - 테이블에 대한 view가 존재하는데.. 테이블이 drop되면 view는 status를 보면 invalid, 상태로 남아있음!(객체는 남아있으나..!)

- 검색 속도를 향상(select 수행 성능향상) 위해서 사용하는 객체

  - b*tree index
    - root node - branch node - leaf node(컬럼값.rowid형태로 인덱스 엔트리들이 저장, 컬럼값의 오름차순)
  - b*map index
  - 단일 컬럼 인덱스
  - 복합 컬럼 인덱스
  - function based index 컬럼표현식의 결과값으로 index 생성

  ```sql
  create index ~ on table(column [desc]);
  -- 변경하려면??
  alter index ~ on table(column....);
  drop index ~ ;
  ```

- sequence

  - 최소값~최대값 범위내에서 설정된 증감값에 따라 정수를 생성하는 객체

  ```sql
  --alter sequence 시퀀스명
  create sequence ~
  increment by ~
  maxvalue ~ |nomaxvalue
  minvalue ~ |nominvalue
  cycle ~ |nocycle
  cache~ |nocache;
  -- 모두 생략가능함....
  alter sequence 시퀀스명 -- 변경하기위해서 그러나 start with 속성은 변경 불가
  
  drop sequence 시퀀스명; -- 메타 정보만 data dictionary로 부터 삭제 됨.
  ```

- Synonym

  - schema, '객체@dblink명' 처럼 긴 객체이름을 간결하게 줄여서 쓰기위한 것
  - 테이블, 뷰, 시퀸스 등 객체 이름 대신 사용할 수 있는 다른 이름을 부여하는 객체임.
    - create public synonym 동의어이름 from 사용자 객체이름; (DBA)
    - create synonym 동의어이름 for schema, 객체@dblink명
  - 삭제는 drop synonym 이름 으로 

- 데이터베이스 접속

  - 대상 데이터베이스에 user명이 등록되어 있어야 하며, 인증방식도 정의되어 있어야함!

    - create session 권한이 있어야 함! 
    - create user ~ -- 권한은 DBA만 가지고 있음(System(sys))
    - identified by 비밀번호
    - default tablespace ~
    - temp tablespace ~
    - tablespace quota XXM
    - Profile ~
    - consumer group ~
    - 위에 있는 것들은 설정하지 않아도 기본값은 있음~~

  - 권한 - 시스템권한과 객체권한이 있음

    - 시스템 권한

      - DBA가 줌

    - 객체 권한

      - 객체의 소유자가 줌(대신에 DBA도 줄수 있음)
        - 권한 부여
          - grant ... on 객체[(컬럼....)]
          - revoke .... on 객체(대상객체명)

    - grant 권한.... to user명.... role명..... public(DBA만 가능)(권한을 줌)

    - ROLE - 특정업무, 직무와 연관된 권한들을 그룹핑한 것

    - revoke 권한..... from user명... roll.public(회수)

    - role 생성권한은 DBA만 가짐.

      - create role 롤이름;

    - 생성된 role 권한을 주는 것

      - grant 시스템권한, 객체 권한 to를 이름;
      - grant 롤이름 to 사용자|롤이름|public;

      