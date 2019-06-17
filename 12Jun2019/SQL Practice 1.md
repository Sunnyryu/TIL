## SQL 연습



##### 1 연습문제

```sql
select *
from emp
where ENAME like '%A'; -- A로 끝나는 사람 문제

select empno, ename, job, sal, deptno
from emp
where job = 'SALESMAN';  --  SALESMAN인 직원 출력

select empno, ename, job, sal, deptno
from emp
where sal > 2000 and deptno = 20
union
select empno, ename, job, sal, deptno
from emp
where sal > 2000 and deptno = 30; -- union을 사용한 부서 20,30번인 직원중 2000이상의 sal을 받은 분들

select empno, ename, job, sal, deptno
from emp
where sal > 2000 and (deptno = 20 or deptno = 30);  -- 집합연사자를 사용하지 않는 방식

select *
from emp
where sal < 2000
union
select *
from emp
where sal > 3000; -- between을 사용하지 않고 나타낸 식

select *
from emp
where comm is null and MGR is not null and job in ('MANAGER', 'CLERK')
minus
select *
from emp
where ename like '_L%'; -- 추가 수당 없고 상급자 있고 직책이 매니저나 서기인 사원중 사원 이름의 두번째 글자가 L이 아닌 사원의 정보 출력

SELECT INSTR('HELLO, ORACLE!', 'L') AS INSTR_1
FROM dual; -- 일반 적으로 했다면 행이 10개라면 10개가 나오지만 dual을 사용하면 1개의 값만 나옴..!!

select *
from emp
where instr(ename, 'S') > 0;
select *
from emp
where ename like '%S%';
-- INSTR를 이용해서 S가 들어간 행 찾기 와 LIKE를 이용해서 S가 들어가는 이름 찾기

select 'KEVIN' AS REPLACE_BEFORE,
    REPLACE('KEVIN', 'V', 'B') AS REPLACE_1
FROM DUAL; -- V를 B로 바꾸는 문제

SELECT EMPNO, ENAME, MGR,
       CASE
          WHEN MGR IS NULL THEN '0000'
          WHEN SUBSTR(MGR, 1, 2) = '78' THEN '1111'
          WHEN SUBSTR(MGR, 1, 2) = '77' THEN '2222'
          WHEN SUBSTR(MGR, 1, 2) = '76' THEN '3333'
          WHEN SUBSTR(MGR, 1, 2) = '75' THEN '4444'
          ELSE TO_CHAR(MGR)
       END AS CHG_MGR
  FROM EMP -- CASE WHEN & THEN을 이용한 문제 풀이
  
  
select deptno, job, count(*), MAX(SAL), SUM(SAL), AVG(SAL)
FROM EMP
group by rollup(deptno, job);

-- Roll up 함수를 적용한 그룹화 (소~ 대 그룹으로rollup은 열에 한하여 결과가 출력된다는 것!)

select deptno, job, count(*), max(sal), sum(sal), avg(sal)
from emp
group by cube(deptno, job)
order by deptno, job;

--cube 함수

select deptno, job, count(*)
from emp
group by grouping sets(deptno, job)
order by deptno, job;
-- grouping 함수

select job, count(*)
from emp
group by job
having count (*) >= 2; -- 2명이상인 직책에 사원이 몇명인지 구하기

select nvl2(comm, 'o', 'x') as exist_comm,
count(*) as cnt
from emp
group by nvl2(comm, 'o', 'x');  -- 추가수당을 받는 지 안받는 지 푸는 문제

select *
from emp, dept
where emp.deptno =dept.deptno
order by empno;

select *
from emp e, dept d
where e.deptno = d.deptno
order by empno; -- join인 것과 아닌 것의 예
select e.empno, e.ename, d.deptno, d.dname, d.loc
from emp e, dept d
where e.deptno = d.deptno
order by d.deptno, e.empno; -- 열이름에 각각의 테이블 이름도 명시할때

select *
from emp e, salgrade s
where e.sal between s.losal and s.hisal; -- 비등가 조인 예제

select e1.empno, e1.ename, e1.mgr,
       e2.empno as mgr_empno,
       e2.ename as mgr_ename
    from emp e1, emp e2
    where e1.mgr = e2.empno; -- 같은 테이블을 두번 사용하여 자체 조인한 것임.\\

select e.empno, e.ename, e.job, e.mgr, e.hiredate, e.sal, e.comm,
deptno, d.dname, d.loc
from emp e natural join dept d
order by deptno, e.empno; -- natural join 예제

select e.empno, e.ename, e.job, e.mgr, e.hiredate, e.sal e.comm,
e.deptno, d.dname, d.loc
from emp e join dept d using(deptno)
where sal >= 3000
order by deptno, e.empno; -- join ~ using

select e.empno, e.ename, e.job, e.mgr, e.hiredate, e.sal e.comm,
e.deptno, d.dname, d.loc
from emp e join dept d on(e.deptn0 = d.deptno)
where sal <= 3000
order by e.deptno, empno; -- join ~ on



```





