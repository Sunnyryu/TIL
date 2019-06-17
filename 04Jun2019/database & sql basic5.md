## DataBase & SQL

#### SQL 함수 복습

- 그룹함수 : 여러행의 컬럼이 함수의 인수로 전달되고, 결과는 1개로 리턴됨.
- 종류 : sum,avg,min,max,count,stddev,varience
- 그룹함수는 null을 연산에 포함시키지 않습니다.
- count(collum) - null이 아닌 계수를 리턴
- count(*) = 테이블의 전체 함수를 리턴, 내부적으로는 not null 또는 pk 제목조건을 씀
- 그룹함수(all | distinct 컬럼)   ( 수행순서)

- select -                                   -------    5
- from -                                      -------    1
- [where 필터조건]                   -------   2
- group by 컬럼, .....                -------     3
- having 그룹함수 조건            -------   4 
- order by 컬럼 정렬방식          -------  6

- 그룹함수를 적용한 컬럼과 그룹함수를 적용하지 않은 컬럼이 있을 경우 select 절에 있을 경우
  - group by 절에 그룹함수를 적용하지 않은 컬럼을 써줘야함
- 그룹함수가 조건은 having절에 선언합니다.

- 검색방법 : projection, selection, join
- join : 하나 이상의 테이블에서 일반적으로는 동일한 속성의 컬럼값이 일치할 때
  - 테이블들의 raw를 결합해서 결과집합으로 생성함
- inner join (equ join)
- non equi join
- self join( 하나의 로우에 2개를 조인함 - 자기참조가 가능한 테이블에서만 수행 가능 )
  - 자기참조가 가능한 것은 pk를 참조하는 것이 있어야함.!
- outer join(일치하는 조인컬럼값이 없거나, 조인컬럼값이 null인 row도 조인 결과로 생성이 필요할 때)
- cartiesian product(조건 조건을 생략하거나, 조인 조건을 논리적으로 잘 못 정의하면 두 테이블의 모든 row가 한번씩 join되는 경우)

- 오라클에서 초기 버전부터 사용했었던 조인 구문
  - where - 조인조건

```sql
EX 1)
selet e.ename, e.deptno. d.dname
from emp e, dept d, -- cartesian product

EX 2) 부서번호가 NULL인 사원데이터를 조건 결과에 포함하려면
select e.name, e.deptno, d.dname
from emp e, dept d
where e.deptno = d.deptno(+); -- 조인할 로우가 없는 쪽에 outer를 해줘야함.

EX 3) SQL 1999에서는
select e.name, e.deptno, d.dname
from emp e, left outer join dept d on e.deptno = d.deptno;

EX 4) 소속 사원이 없는 부서정보를 조인 결과에 포함하려면
select e.ename, e.deptno, d.deptno
from emp e right outer join dept d on e.deptno = d.deptno;

EX 5) 양족다 outer가 필요한겨우
select e.ename, e.deptno, d.deptno
from emp e full outer join dept d on e.deptno = d.deptno;
```



- sql1999 조인 구문
- natural join ( from tab1 a natural join tab1 a)
  - oracle 서버가 조인할 테이블에서 동일한 이름의 컬럼으로 자동 equi 방식 조인을 수행함
  - 조인할 테이블에서 동일한 이름의 컬럼 앞에 소유자 테이블명 또는 alias를 선언하지 않음.
  - 동일한 속성이지만, 설계할때 부모와 자식 테이블에서 이름을 다르게 정의하면 조인 수행안함.
- join .. using
  - from tab1 a join tab a using (조인컬림명)
- join ... on
  - from tab1 aa join tbs 2 on a.col=bcol2
- self join도 join on을 사용하는데 from절이 2번 옴.



#### 서브쿼리

- 조건 값을 알 수 없어 query를 2번 사용할 경우에 쓰임
- subquery = inner query= nested query
- Selct의 절과 집합 = ResultSet = cursor
- Query Block을 outer quary 나 Main Quary라고 함
- 서브쿼리는 select 안 select 안이나 from 절, where 절, having 절,order by절에 쓰임
- where절과 having절의 subquery는 연산자 오른쪽에 () 안에 정의합니다.
- 서브 커리의 종류
  - 단일 행을 리턴하는 subquery : single row subquery
    - where절에 single row subquery 를 사용할 경우,
    -  반드시 single row operator(>, >=, <=, <, =, <>)와 함께 사용함
  - 복수행을 리턴하는 subquery : multiple row subquery
    - where절에 multiple row subquery를 사용할 경우,
    - 반드시 multiple row operator(In, any, all)와 함께 사용함
      - multiple row subquery의 값을 =, or로 비교하려면 in 연산자를 사용함
      - multiple row subquery의 값이 최소 1명 이상 높거나 클 때를 만드려면 any를 씀
      - multiple row subquery의 값이 가장 높거나 클 때를 만드려면 all를 씀
    - multiple column subquery, pair-wise 비교를 사용해야 할 때가 있음
  - 단일 행, 단일 컬럼값을 리턴 subquery : scalar subquery
  - 두개 이상의 컬럼값을 리턴하는 subquery : multiple column subquery
  - subquery에 그룹함수를 사용할 수 있음.
  - subquery의 select구문에 order by절을 제외한 모든 구문을 쓸 수 있음.
  - where절의 조건마다 subquery로 적용 가능함
  - from절의 subquery를 inline view라고 부름

```sql
--subquery의 모든 값을 비교해야 하는 연산에서는 null이	 포함되어 있는지 
-- 여부를 먼저 체크해서 null을 처리하거나 제외시켜야 합니다.
select empno
from emp
where empno not in (select mgr
                   from emp
                   where mgr is not null);
```

```sql
-- 예제를 이용하여 이해하기
-- ex 1)
-- 문> 각 부서별로 평균급여보다 급여를 많이 받는 사원 검색 (이름, 부서, 급여) - corelated subquery, join

select a.ename, a.deptno, a.sal
from emp a , (select deptno, avg(sal) avgsal
             from emp
             group by deptno) b
where a.deptno = b.deptno
and a.sal > b.avgsal;



select a.ename, a.deptno, a.sal
from emp a
where  a.sal  > (select avg(sal) 
                 from emp  
                 where a.deptno = deptno);


desc employees  --현재 근무부서와 직무
desc job_history --과거 근무했었던 부서, 직무, 기간
-- ex 2)사원들 중에서 2번이상 부서 또는 직무를 변경한 이력이 있는 사원의 사번, 이름(last_name) 출력하시오

select a.employee_id, a.last_name
from employees a, (select employee_id, count(employee_id) cnt
                   from job_history
                   group by employee_id) b
where a.employee_id = b.employee_id
and b.cnt >=2;


select a.employee_id, a.last_name
from employees  a                     
where 2 <=  (select count(employee_id)
             from job_history
             where a.employee_id =employee_id);
 


※where exists (co-related subquery)

-- ex 3)subquery를 사용해서 관리자인 사원들만 검색
select empno
from emp a
where exists (select '1'
              from emp 
              where a.empno = mgr);


-- ex 4) 문>subquery를 사용해서 관리자가 아닌 사원들만 검색
select empno
from emp a
where not exists(select '1'
                   from emp 
		 where a.empno = mgr);


conn hr/oracle
-- ex 5) 부서별 총 급여가 전체 부서의 평균급여보다 큰 부서번호와 총급여를 출력합니다.

with 
dept_sum as (select department_id, sum(salary) sum_sal
             from employees
             group by department_id),
emp_avg as (select avg(sum_sal) total_avg
             from dept_sum)
select a.department_id, a.sum_sal
from dept_sum a, emp_avg b
where a.sum_sal > b.total_avg;

```

- 집합 연산자 
- union , union all, minus, intersect이 쓰임
- 각각의 select문의 컬럼개수와 타입은 일치해야 합니다.
- order by절은 마지막 select문에 선언 가능합니다.
- rollup은 전체짓기와 서브짓기를 이용함..
  - ex) group by rollup (a,b,c)
    - group by r(a,b,c)
      - group by (a,b)
        - group by(a)
          - group()
- cube는 rollup과 쪼금 다름
  - group by cube (a,b,c),(a,b),(a,c),(b,c),(a),(b),(c),()
    - group by (a,b,c),(a,b),(a,c),(b,c),(a),(b),(c),()
      - group by (a,b)(b,c)(a,c)(a)(b)(c)()
        - group by(a )(b)(c)()
          - group by()





