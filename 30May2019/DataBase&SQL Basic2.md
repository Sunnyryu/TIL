## DataBase & SQL

#### SQL

- 조건문 이용하기

```sql
--select 검색 컬럼 리스트, 표현식
--from 테이블
--where 조건 ; => 컬럼 비교연산자 값 ( >, <, >=, =, !=, <>, <=)

--부서 번호 30번인 사원 검색
select ename, deptno
from emp
where deptno = 30;


--직무가 ANALYST인 사원 검색
select ename, job
from emp
where job = 'ANALYST'   --컬럼값은 대소문자 구별합니다.


--급여가 3000이상인 사원 검색
select ename, sal
from emp
where sal >= 3000

--empno 사번
--ename 이름
--job 직무
--hiredate 입사날짜
--comm   커미션
--deptno 부서번호
--sal 급여
--mgr 관리자번호

alter session set nls_date_format='RR/MM/DD';

--Quiz> 87년 1월 1일이후에 입사한 사원 이름 검색
select empno, ename, hiredate
from emp
where hiredate >= '87/01/01';

select empno, ename, hiredate
from emp
where hiredate >= '87년01월01일'; -- error

--날짜는 session설정 날짜 포맷과 일치하면 자동으로 conversion해줍니다.
--날짜는 session설정 날짜 포맷과 일치하지 않으면 오류 발생합니다.


--문> 커미션을 받는 사원을 검색하시오
select ename, comm
from emp 
where comm != null;   --> 문법 오류가 아닌 논리 오류?

select ename, comm
from emp 
where comm is not null;

select ename, comm
from emp 
where comm > 0;

--문> 커미션을 받지 않는 사원을 검색하시오
select ename, comm
from emp 
where comm = null;   --> 문법 오류가 아닌 논리 오류?

※ is null, is not null 연산자 : null 비교 연산자

select ename, comm
from emp 
where comm is null;

논리연산자 and,  or, not

--문> 월급이 3000이상 5000이하인 사원 검색 (3000 포함, 5000포함)
select ename, sal
from emp
where  sal >= 3000 and sal <=5000;

--※ 범위 연산자  between 하한값 and 상한값

select ename, sal
from emp
where  sal between 3000 and  5000;


--문> 직무가 clerk 또는 analyst인 사원 검색
select ename, job
from emp
where job ='CLERK' or job='ANALYST';


--※ in 리스트 연산자 : in (값, 값, 값,....)
select ename, job
from emp
where job in ('CLERK' ,'ANALYST');


--※ character pattern matching 연산자 : like '%, _'
--%는 문자 종류는 모든 문자, 개수는 0~M
--_는 문자 종류는 모든 문자, 개수는 1을 의미합니다.
----문> 사원이름중에서 두번째 문자가 'D'인 사원 검색
select ename
from emp
where ename like '_D%';

--문> 사원이름중에서 첫번째 문자가 'S'로 시작하는 사원 검색
select ename
from emp
where ename like 'S%';

--문> 사원이름중에서 문자가 'N'로 끝나는 사원 검색
select ename
from emp
where ename like '%N';


--문> 81년도에 입사한 사원 검색
select ename, hiredate
from emp
where  hiredate like '81%';

select ename, hiredate
from emp
where  hiredate between '81/01/01' and '81/12/31';


select ename, hiredate
from emp
where  hiredate > '80/12/31' 
and hiredate < '82/01/01';


--논리연산자의 우선순위 NOT, AND, OR

--문>업무가 PRESIDENT이고 급여가 1500 이상이거나 업무가 SALESMAN인 사원의
 --사원번호, 이름, 업무, 급여를 출력하여라.
select empno, ename, job, sal
from emp
where (job =' PRESIDENT' and sal >= 1500) or job= 'SALESMAN';

--문> 급여가 1500 이상이고, 업무가 SALESMAN이거나 PRESIDENT인 사원의
-- 사원번호, 이름, 업무, 급여를 출력하여라.

select empno, ename, job, sal
from emp
where sal >= 1500 and job in (' PRESIDENT', 'SALESMAN);


select empno, ename, job, sal
from emp
where sal >= 1500 and job =' PRESIDENT' or job= 'SALESMAN);
```

- select -(필수)
- from -(필수)
- [where 필터 조건]
- [group by 컬럼(절)]
- [having 조건]
- [order by 정렬기준컬럼 정렬방식]  -asc 오름차순, default, -desc 내림차순

```sql
--문> 월급의 오름차순으로 사원 정보 출력
select ename, job, sal
from emp
order by sal ;

select ename, job, sal
from emp
order by sal desc;

--문> 사원들의 사번, 이름, 부서번호, 월급, 커미션, 연봉(sal+comm*12)의 결과 
--출력 , 연봉의 내림차순으로...


select empno, ename, deptno, sal, comm, (sal+nvl(comm, 0))*12 "연봉"
from emp
order by (sal+nvl(comm, 0))*12 desc;

select empno, ename, deptno, sal, comm, (sal+nvl(comm, 0))*12 "연봉"
from emp
order by "연봉" desc;

select empno, ename, deptno, sal, comm, (sal+nvl(comm, 0))*12 "연봉"
from emp
order by 6 desc   ;

--order by절에는 컬럼 표현식, 별칭, 컬럼 포지션을 사용할 수 있습니다.

--문> 사원들의 사번, 이름, 부서번호, 월급, 커미션, 연봉(sal+comm*12)의 결과 
--출력 (부서번호로 오름차순 정렬하고, 연봉의 내림차순으로...)

select empno, ename, deptno, sal, comm, (sal+nvl(comm, 0))*12 "연봉"
from emp
order by depno, 6 desc;

select empno, ename, deptno, sal, comm, (sal+nvl(comm, 0))*12 "연봉"
from emp
order by 3 asc, "연봉" desc;
```







