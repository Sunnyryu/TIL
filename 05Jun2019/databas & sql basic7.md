## DataBase & SQL

시스템 함수

```sql
-- ex) 예시
--> emp 테이블에서 사원이름, 직무, 급여 데이터와 전체 사원의 급여가 높은 순서의 순위를 rank(), dense_rank(), row_number()로 출력하시오
select  ename, job, sal, 
        dense_rank( ) over ( order by sal desc ) sal_rank
        ,  rank( ) over ( order by sal desc ) sal_rank2
        ,  row_number( ) over ( order by sal desc ) sal_rank2
from emp; 



-- emp 테이블에서 관리자로 파티셔닝된 사원이름, 오름차순 정렬된 급여 데이터 누적 합 출력
select  ename, mgr, sal, sum(sal) over (partition by mgr order by sal) 
from emp;


-- emp 테이블에서 관리자로 파티셔닝된 사원이름, 오름차순 정렬된 급여 데이터 누적 합 출력
select  ename, mgr, sal, 
        sum(sal) over (partition by mgr order by sal
                       range  unbounded preceding) 
from emp;

-- emp 테이블에서 관리자로 파티셔닝된 사원이름, 오름차순 정렬된 급여 데이터의 행 기준 누적 합 출력
select  ename, mgr, sal, 
        sum(sal) over (partition by mgr order by sal
                       rows between unbounded preceding and current row   ) 
from emp;


-- emp 테이블에서 관리자로 파티셔닝된 사원이름, 오름차순 정렬된 급여 데이터의 행 기준으로 현재행의 앞에 한행, 뒤에 한 행의 누적 합 출력
select  ename, mgr, sal, 
        sum(sal) over (partition by mgr order by sal
                       rows between 1 preceding and 1 following   ) 
from emp;

-- emp 테이블에서 관리자로 파티셔닝된 사원이름, 오름차순 정렬된 급여 데이터의 행 기준으로 급여의 -200~+200 범위의 급여자 수 출력
select  ename, mgr, sal, 
        count(sal) over (order by sal
                         range between 200 preceding and 200 following   ) 
from emp;




select  ename, mgr, sal, 
        first_value(sal) over (partition by mgr order by sal ) ,
        last_value(sal) over (partition by mgr order by sal ) 
from emp;


select  ename, mgr, sal, 
        first_value(sal) over (partition by mgr order by sal ) ,
        last_value(sal) over (partition by mgr order by sal 
        range between current row and  unbounded following ) 
from emp; 



select  ename, hiredate, sal, 
        lag(sal) over (order by hiredate ) ,
        lag(sal, 2, 0) over (order by hiredate ) 
from emp;


select  ename, hiredate, sal, 
        lead(sal) over (order by hiredate ) ,
        lead(sal, 2, 0) over (order by hiredate ) 
from emp;

```

