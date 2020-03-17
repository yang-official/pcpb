# Chapter 1: Select

#### 1.1 Second Highest Salary
```
Table: Employee
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```
Write a SQL query to get the second highest salary in the above table `Employee`. If there is no second highest salary, the query should return `null`.
```
+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+
```
Source: LC 176

Solution
```SQL
select max(Salary) as SecondHighestSalary
from Employee
where Salary < (
  select max(Salary) from Employee
);
```
#### 1.2 Nth Highest Salary
```
Table: Employee
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```
Write a SQL query to get the nth highest salary from the above `Employee` table. If there is no nth highest salary, the query should return `null`.
```
+------------------------+
| getNthHighestSalary(2) |
+------------------------+
| 200                    |
+------------------------+
```
Source: LC 177

Solution using variables for MySQL
```SQL
set N = N - 1;
select distinct Salary
from Employee
order by Salary desc
limit 1 offset N;
```

Solution using dense_rank()
```SQL
begin
select distinct Salary into result
from (
  select Salary, dense_rank() over (order by Salary desc) rank from Employee
)
where rank = N;
exception when no_data_found then result := null;
end;
```
