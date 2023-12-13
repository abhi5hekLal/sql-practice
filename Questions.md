1. Write an SQL query to fetch “FIRST_NAME” from Worker table using the alias name as <WORKER_NAME>.

```sql
SELECT first_name AS worker_name
FROM worker;
```

2. Write an SQL query to fetch “FIRST_NAME” from Worker table in upper case.

```sql
SELECT UPPER(first_name) 
FROM worker;
```
3. Write an SQL query to fetch unique values of DEPARTMENT from Worker table.

```sql

```
4. Write an SQL query to print the first three characters of  FIRST_NAME from Worker table.


```sql
select substring(first_name, 1, 3) from worker;
```
5. Write an SQL query to find the position of the alphabet (‘b’) in the first name column ‘Amitabh’ from Worker table.


```sql
select INSTR(first_name, 'B') from worker where first_name = 'Amitabh';
```
6. Write an SQL query to print the FIRST_NAME from Worker table after removing white spaces from the right side.


```sql
select RTRIM(first_name) from worker;
```
7. Write an SQL query to print the DEPARTMENT from Worker table after removing white spaces from the left side.


```sql
select LTRIM(first_name) from worker;
```
8. Write an SQL query that fetches the unique values of DEPARTMENT from Worker table and prints its length.


```sql
select distinct department, LENGTH(department) from worker;
```
9. Write an SQL query to print the FIRST_NAME from Worker table after replacing ‘a’ with ‘A’.


```sql
select REPLACE(first_name, 'a', 'A')  from worker;
```
10. Write an SQL query to print the FIRST_NAME and LAST_NAME from Worker table into a single column COMPLETE_NAME.
space char should separate them.


```sql
select CONCAT(first_name, ' ', last_name) AS COMPLETE_NAME from worker;
```
11. Write an SQL query to print all Worker details from the Worker table order by FIRST_NAME Ascending.


```sql
select * from worker ORDER by first_name;
```
12. Write an SQL query to print all Worker details from the Worker table order by 
RST_NAME Ascending and DEPARTMENT Descending.


```sql
select * from worker order by first_name, department DESC;
```
13. Write an SQL query to print details for Workers with the first name as “Vipul” and “Satish” from Worker table.


```sql
select * from worker where first_name IN ('Vipul', 'Satish');
```
14. Write an SQL query to print details of workers excluding first names, “Vipul” and “Satish” from Worker table.


```sql
select * from worker where first_name NOT IN ('Vipul', 'Satish');
```
15. Write an SQL query to print details of Workers with DEPARTMENT name as “Admin*”.


```sql
select * from worker where department LIKE 'Admin%';
```
16. Write an SQL query to print details of the Workers whose FIRST_NAME contains ‘a’.


```sql
select * from worker where first_name LIKE '%a%';
```
17. Write an SQL query to print details of the Workers whose FIRST_NAME ends with ‘a’.


```sql
select * from worker where first_name LIKE '%a';
```
18. Write an SQL query to print details of the Workers whose FIRST_NAME ends with ‘h’ and contains six alphabets.


```sql
select * from worker where first_name LIKE '_____h';
```
19. Write an SQL query to print details of the Workers whose SALARY lies between 100000 and 500000.


```sql
select * from worker where salary between 100000 AND 500000;
```
20. Write an SQL query to print details of the Workers who have joined in Feb’2014.


```sql
select * from worker where YEAR(joining_date) = 2014 AND MONTH(joining_date) = 02;
```
21. Write an SQL query to fetch the count of employees working in the department ‘Admin’.


```sql
select department, count(*) from worker where department = 'Admin';
```
22. Write an SQL query to fetch worker full names with salaries >= 50000 and <= 100000.


```sql
select concat(first_name, ' ', last_name) from worker
where salary between 50000 and 100000;
```
23. Write an SQL query to fetch the no. of workers for each department in the descending order.


```sql
select department, count(worker_id) AS no_of_worker from worker group by department
ORDER BY no_of_worker desc;
```
24. Write an SQL query to print details of the Workers who are also Managers.


```sql
select w.* from worker as w inner join title as t on w.worker_id = t.worker_ref_id where t.worker_title = 'Manager';
```
25. Write an SQL query to fetch number (more than 1) of same titles in the ORG of different types.


```sql
select worker_title, count(*) as count from title group by worker_title having count > 1;
```
26. Write an SQL query to show only odd rows from a table.


```sql
slect * from worker where MOD (WORKER_ID, 2) != 0; 
select * from worker where MOD (WORKER_ID, 2) <> 0;
```
27. Write an SQL query to show only even rows from a table. 


```sql
select * from worker where MOD (WORKER_ID, 2) = 0;
```
28. Write an SQL query to clone a new table from another table.

select * from worker_clone;

```sql
CREATE TABLE worker_clone LIKE worker;
INSERT INTO worker_clone select * from worker;
```
29. Write an SQL query to fetch intersecting records of two tables.


```sql
select worker.* from worker inner join worker_clone using(worker_id);
```
30. Write an SQL query to show records from one table that another table does not have.



```sql
select worker.* from worker left join worker_clone using(worker_id) WHERE worker_clone.worker_id is NULL;
```
31. Write an SQL query to show the current date and time.
AL


```sql
select curdate();
select now();
```
32. Write an SQL query to show the top n (say 5) records of a table order by descending salary.


```sql
select * from worker order by salary desc LIMIT 5;
```
33. Write an SQL query to determine the nth (say n=5) highest salary from a table.


```sql
select * from worker order by salary desc LIMIT 4,1;
```
34. Write an SQL query to determine the 5th highest salary without using LIMIT keyword.


```sql
select salary from worker w1
WHERE 4 = (
SELECT COUNT(DISTINCT (w2.salary))
from worker w2
where w2.salary >= w1.salary
);
``` 
35. Write an SQL query to fetch the list of employees with the same salary.


```sql
select w1.* from worker w1, worker w2 where w1.salary = w2.salary and w1.worker_id != w2.worker_id;
```
36. Write an SQL query to show the second highest salary from a table using sub-query.


```sql
select max(salary) from worker
where salary not in (select max(salary) from worker);
```
37. Write an SQL query to show one row twice in results from a table.


```sql
select * from worker
UNION ALL
select * from worker ORDER BY worker_id;
```
38. Write an SQL query to list worker_id who does not get bonus.
select worker_id from worker where worker_id not in (select worker_ref_id from bonus);

```sql

```
39. Write an SQL query to fetch the first 50% records from a table.
select * from worker where worker_id <= ( select count(worker_id)/2 from worker);

```sql

```
40. Write an SQL query to fetch the departments that have less than 4 people in it.
select department, count(department) as depCount from worker group by department having depCount < 4;

```sql

```
41. Write an SQL query to show all departments along with the number of people in there.
select department, count(department) as depCount from worker group by department;

```sql

```
42. Write an SQL query to show the last record from a table.
select * from worker where worker_id = (select max(worker_id) from worker);

```sql

```
43. Write an SQL query to fetch the first row of a table.
select * from worker where worker_id = (select min(worker_id) from worker);

```sql

```
44. Write an SQL query to fetch the last five records from a table.
(select * from worker order by worker_id desc limit 5) order by worker_id;

```sql

```
45. Write an SQL query to print the name of employees having the highest salary in each department.
select w.department, w.first_name, w.salary from
 (select max(salary) as maxsal, department from worker group by department) temp
inner join worker w on temp.department = w.department and temp.maxsal = w.salary;

```sql

```
46. Write an SQL query to fetch three max salaries from a table using co-related subquery
select distinct salary from worker w1
where 3 >= (select count(distinct salary) from worker w2 where w1.salary <= w2.salary) order by w1.salary desc;
Y RUN AFTER REVISING THE CORELATED SUBQUERY CONCEPT FROM LEC-9.
select distinct salary from worker order by salary desc limit 3;

```sql

```
47. Write an SQL query to fetch three min salaries from a table using co-related subquery
select distinct salary from worker w1
where 3 >= (select count(distinct salary) from worker w2 where w1.salary >= w2.salary) order by w1.salary desc;

```sql

```
48. Write an SQL query to fetch nth max salaries from a table.
select distinct salary from worker w1
where n >= (select count(distinct salary) from worker w2 where w1.salary <= w2.salary) order by w1.salary desc;

```sql

```
49. Write an SQL query to fetch departments along with the total salaries paid for each of them.
select department , sum(salary) as depSal from worker group by department order by depSal desc;

```sql

```
50. Write an SQL query to fetch the names of workers who earn the highest salary.
select first_name, salary from worker where salary = (select max(Salary) from worker);
```sql

```
