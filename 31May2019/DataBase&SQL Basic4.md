## DataBase & SQL

#### SQL 함수

- Null 처리(기타 단일 행 함수 종류)

  - nvl(column, expression) = null이 아니면 column을, null이면 값(expression)을 호출
  - nvl2(column, expression1, expression2) = column값이 null이 아니면 expression1으로 호출 하고 null이면 expression2로 호출함 
    - expression1과 expression2은 동일한 타입이여야 합니다.
  - coalesce(column, expression1, expression2, ... expression255) 
    - column값이 null이면 expression을 실행하고 그 것도 null이면 null 아닌 값이 나올 때까지 반복해서 null이 아닌 값이 나올 때까지 진행!
  - nullif(expression1, expression2)
    - expression1과 expression 값이 동일하면 null 리턴
    - expression1과 expression 값이 동일하지 않으면 expression1 리턴
  - 조건처리 함수 : decode(column, 표현식1, 리턴값 함수, 같지 않으면 표현식2와 비교하여 리턴값2를 가짐 
  - 조건처리 표현식 , 표준 sql3 : case [표현식] when [값|조건표현식] then 값 else end

- 그룹함수

  - 그룹핑된 행 집합, 테이블의 전체 행 집합의 컬럼이 함수의 인수로 전달되고 결과는 반드시 1개 리턴
    - sum(number타입|expression)
    - avg(number타입|expression)
    - min(number, char, date 컬럼타입|expression)
    - max(number, char, date 컬럼타입|expression)
    - count(|distint|number, char, date 컬럼타입|expression) : null 이 아닌 값을 카운트함
    - stddev(number:타입|expression) : 표준편차
    - variance(number타입|expression) : 분산

  - group by는 그룹화가 안된 것을 그룹화 시켜주는 용어임.
  - group by절에는 column명만 선언할 수 있습니다.
  - 그룹함수의 조건은 having절에 선언합니다. having절은 group by절과 함께 사용됩니다.

- 검색방법

  - Projection, selection, join

```sql
--oracle join syntax - where절에 조인조건 선언
--sql1999 표준 syntax  -  from절에 조인조건 선언

--equi join (inner join)
--non-equi join
--self-join (자기참조가 가능한 테이블에서만)
--※ 조인 조건을 잘못 정의하거나 , 조인 조건을 누락하면 cartesian product (cross join)
--outer join (조인컬럼값이 null인 경우 결과집합에 포함시키기 위한 조인)

select a.last_name, a..department_id, b.department_name
from  employees a, departments b;  ---? 20명의 사원 데이터 (20*8)rows, cartesian join = 160개 나옴

select a.last_name, a.department_id b.department_name
from employees a, departments b
where a.department_id = b.department_id;

select a.last_name, a.department_id, b.department_name
from  employees a natural join  departments b;  -->?
--natual join 은 oracle 서버가 조인할 테이블에서 동일한 이름의 컬럼으로 자동 equi 방식 조인을 수행합니다.
--natual join 은 조인할 테이블에서 동일한 이름의 컬럼 앞에 소유자 테이블명 또는 alias를 선언하지 않습니다.
--natual join 은 동일한 속성이지만, 설계할때 부모와 자식 테이블에서 이름을 다르게 정의하면 조인 수행 안됩니다

create table  copy_emp
as select  empno , ename, job, hiredate, sal, mgr, deptno deptid
from emp;

desc  copy_emp
select * from copy_emp;

문> copy_emp와 dept테이블에서 사번, 이름, 부서번호, 부서명 출력
select a.empno, a.ename, b.deptno, b.dname
from copy_emp a  join  dept b  on a.deptid = b.deptno;


drop table copy_emp purge;  --테이블 삭제

desc salgrade
desc emp

문> 사원이름, 급여, 급여의 등급을 조회 출력  --non-equi join으로 해결
select a.ename, a.sal, b.grade
from emp a, salgrade b
where a.sal between b.losal and b.hisal;

select a.ename, a.sal, b.grade
from emp a join  salgrade b  on a.sal between b.losal and b.hisal;
 

select a.empno, a.ename, b.deptno, b.dname
from emp a  inner join  dept b  on a.deptno = b.deptno;
-- 위에 것을 하지 않으면 아래것이 안켜질 수 있음.

--문> 사원번호 사원이름 관리자번호 관리자이름을 조회결과 출력 --self join
select a.empno, a.ename, a.mgr , b.ename
from  emp a, emp b
where a.mgr = b.empno;

select a.empno, a.ename, a.mgr , b.ename
from  emp a join emp b  on a.mgr = b.empno;


conn hr2/oracle
desc employees
desc departments
desc locations
--※ n개의 테이블을 조인할때 최소 조인 조건은  n-1개 
--문> 사원이름 , 소속 부서이름, 부서가 위치한 도시를 조회 출력
select a.last_name, b.department_name, c.city
from employees a, departments b, locations c
where a.department_id = b.department_id
and b.location_id = c.location_id;

select a.last_name, b.department_name, c.city
from employees a join  departments b on a.department_id = b.department_id
join locations c  on   b.location_id = c.location_id;


conn scott/oracle
insert into emp (empno, ename) values (8000, 'Hong');
commit;

--문> 부서번호가 없는 사원을 포함해서 사원들의 부서이름를 함께 출력
select a.empno, a.ename, a.deptno, b.dname
from emp a, dept b
where a.deptno = b.deptno;   --8000번 hong사원 누락됨

select a.empno, a.ename, a.deptno, b.dname
from emp a, dept b
where a.deptno = b.deptno(+); ----8000번 hong사원 포함?

--문> 부서정보를 기준으로 부서의 소속 사원을 출력하고,
--소속 사원이 없는 부서도 출력합니다.
select b.deptno, b.dname, a.empno, a.ename, 
from emp a, dept b
where a.deptno = b.deptno
order by  b.deptno;   ---40번 부서정보 누락?


select b.deptno, b.dname, a.empno, a.ename, 
from emp a, dept b
where a.deptno(+) = b.deptno
order by  b.deptno;  ------40번 부서정보 포함?


select b.deptno, b.dname, a.empno, a.ename, 
from emp a right outer join dept b on a.deptno  = b.deptno
order by  b.deptno; 


-- 문>  부서번호가 없는 사원을 포함하고, 소속 사원이 없는 부서도
--사원들의 사번, 이름, 부서번호, 부서이름를 함께 출력합니다.

select b.deptno, b.dname, a.empno, a.ename, 
from emp a, dept b
where a.deptno(+) = b.deptno(+)
order by  b.deptno;  -- outer 연산자는 양쪽에 선언 불가, 오류 


select b.deptno, b.dname, a.empno, a.ename, 
from emp a full outer join dept b on a.deptno  = b.deptno
order by  b.deptno; -- fullouter는 양쪽 선언된 아이임.
```

