## DataBase & SQL

#### SQL 함수

- 함수 - SQL을 더 강력한 사용을 보조함

  - predefine - db 벤더 nvl, sysdate, user
  - custom(PLSQL)

  

- 단일 행 함수

  - DB의 함수 : 반드시 1개의 결과 리턴

- 복수 행 함수(그룹 함수)

  - 여러개의 값을 받아서 1개의 결과를 리턴

- 분석함수(window 함수)

  - 한 곳에 모든 데이터를 모았는데, 이를 데이터 웨어하우스, 관리하는 것을 데이터 웨어하우징이라 부르는데,
  -  데이터웨어하우징분야에서 사용되는 함수

- Character
- Number
- Date
- Null 처리

```sql
select initcap(ename), lower(ename), upper(ename)
from emp;

select length('korea') length('대한민국')
from dual;

select lengthb('korea') lengthb('대한민국')
from dual;

--함수 안에 함수를 nested하면  nested된 함수부터 처리
select concat(concat(ename, ' is '), job)
from emp;


select substr('today is 2015년 4월 26일', 1, 5), --1에서부터 5개
       substr('today is 2015년 4월 26일', 10, 5), -- 10에서 부터 5개
       substr('today is 2015년 4월 26일', 15),-- 15에서 부터 전부
       substr('today is 2015년 4월 26일', -3, 2) -- 뒤에서 3번쨰부터 2개
from dual;

select instr('korea is wonderful', 'o'), -- O 갯수 2RO
       instr('korea is wonderful', 'o', 1, 2), -- 1에서 2번쨰의 O의 위치
       instr('korea is wonderful', 'o', 9), --9에서 O의 위치
       instr('korea is wonderful', 'x') -- X갯수가 없어 0
from dual;


--#lpad : left padding,  
--#rpad : right padding
--#문자열로 변환, 문자열 전체 길이내에 왼쪽 공백에 특정 문자를 padding

select ename, sal, lpad(sal, 10, '*')-- 10자리 문자열로 만드는데 왼쪽에 부족한 별을 넣음
from emp;

select ename, sal, rpad(sal, 10, '*')-- 10자리 문자열로 만드는데 왼쪽에 부족한 별을 넣음
from emp;

--trim, ltrim, rtrim 함수 rtrim trim은 특정 문자제거, ltrim은 왼쪽 특정문자 제거, rtrim 오른쪽 특정문자 --제거
select length('  hello  '),  length(trim('  hello  '))
from dual; -- 공백 포함 9개/ 공백제외 5개

select trim('H' from 'Hello wonderful'), trim('l' from 'Hello wonderful')
from dual; -- H제거/ 뒤의 l제거 중간에 ll은 제거 못함

select ltrim('Hello wonderful', 'He' ), rtrim( 'Hello wonderful' , 'ful')
from dual; -- He 제거 / ful 제거

select replace('Jack AND Jue', 'J', 'BL')
from dual; -- J를 BL로 바뀜

#translate
-- #########################number function########################

select round(12.345, 2), round(12.345, 0), round(12.345, -1)
from dual; -- 12.35 / 12 / 10

select trunc(12.345, 2), trunc(12.345), trunc(12.345, -1)
from dual; -- 12.34 / 12 / 10

select mod(99, 4)
from dual; -- 3

select ceil(12.345), floor(12.345) from dual;
-- 13/ 12
select power(3, 2), power(5, 2)
from dual; -- 9 / 25




--where절에 함수 사용 가능


--#########################date function########################
timestamp컬럼 타입 (YYYY/MM/DD HH24:MI:SS.SSSSSSSSS)
timestamp(3)  #6이 default
timestamp with time zone

select sessiontimezone from dual;
alter session set time_zone='+3:00';
select sessiontimezone from dual;


--sysdate 시스템의 현재 리턴
--current_date 세션의 timezone기반 현재시간을 date타입으로 리턴
--current_timestamp 세션의 timezone기반 현재시간을 timestamp타입으로 리턴
select   sysdate, current_date, current_timestamp
from dual;

--#add_months(date, n) - 개월 수를 더한 날짜가 리턴
--#months_between(date, date) - 기간이 리턴

select add_months(sysdate, 6)
from dual;--6을 더함

select hiredate, add_months(hiredate, 6)
from emp;-- 고용일 부터 6개월을 더함

select months_between(sysdate, hiredate)
from emp; -- 두가지의 차이를 계산

# next_day(date, '요일명')
select next_day(sysdate, '목')
from emp; --다음 목요일이 몇일인지.



alter session set nls_date_format ='RR/MM/DD';

--trunc, round 
select trunc(to_date('14/02/14'), 'MONTH'), 
       trunc(to_date('14/02/14'), 'YEAR')
from dual; -- 버림은 무조건1월이나 1일로 바꿔줌


select round(to_date('14/02/14'), 'MONTH'), 
       round(to_date('14/02/14'), 'YEAR')
from dual;-- 반올림은 월 기준으로 1~15는 1로 16~31은 다음달 1일로 년기준도 1~6은 1월로 7~12는 내년 1월로 

#last_day(date)
select last_day(to_date('14/02/14')), last_day(to_date('2000/02/14'))
       , last_day(to_date('2100/02/14'))
from dual; -- 마지막날을 확인해주는 것


--문> 사원들의 입사 날짜로부터 6개월후날짜로부터 다음 금요일이 연봉 조정 
--면담날짜입니다. 
--사원들의 사번과 입사날짜와 연봉 조정 면담날짜를 출력하세요
select empno, hiredate, next_day(add_months(hiredate, 6), '금') "연봉조정날짜"
from emp; 

--to_date
--to_char
--to_number 
--ex) '10' + '10' = '20'

-- char - > number = to_number
-- number - > char = to_char
-- char - > date = to_date
-- date - > char = to_char

select to_char(123456.789, '$9,999,999.9999')
from dual; -- 123,456.789

--select to_number('$1,234,567.999', '9,999,999.999')
--from dual; error가 발생함 / 자릿수가 맞지 않음


select to_number('$1,234,567.999', '$99,999,999.9999')
from dual;  --1234567.999가 나옴

select sysdate,  to_char(sysdate, 'YYYY"년" MM"월"  DD"일" DY')
from dual; -- 2019년 05월 30일 목이 나옴

alter session set nls_language=american; -- 아메리칸 타입으로 바꿔줌

select sysdate,  to_char(sysdate, 'Year Month DDspth Day')
from dual;-- Twenty Nineteen May

alter session set nls_language=korean; -- 한국어로 바꿈

select '2019-05-30 5:43 PM' 
       , to_date('2019-05-30 5:43 PM' 'HH12:MI AM YYYY-MM-DD')
from dual;  --error?


select '2019-05-30 5:43 PM' 
       , to_date('2019-05-30 17:43' , 'YYYY-MM-DD HH24:MI')
from dual;   --변환이 정상적으로 수행되면 세션 포맷형식으로 출력됨

  
RR/MM/DD



```







