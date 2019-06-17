```sql
select last_name, hire_date
from employees
where department_id = (select department_id from employees where last_name = 'Zlotkey')
intersect
select last_name, hire_date
from employees
where last_name not like ('Z%'); 

select last_name, hire_date
from employees
where department_id = (select department_id from employees where last_name = 'Zlotkey') and last_name <> 'Zlotkey';


select employee_id, last_name, salary
from employees
where salary >= (select avg(salary) from employees)
order by salary desc;

select employee_id, last_name
from employees
where department_id in (select department_id from employees where last_name like ('%u%'));

select last_name, department_id, job_id
from employees
where 
department_id in (select department_id from departments where location_id = '1700');

select last_name, salary
from employees
where last_name in (select last_name from employees where manager_id = 100);

select department_id, last_name, job_id
from employees
where department_id = (select department_id from departments where department_name = 'Executive'); 

select employee_id, last_name, salary
from employees
where salary >= (select avg(salary) from employees) and department_id in (select department_id from employees where last_name like '%u%');
```

