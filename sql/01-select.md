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

#### 1.3 Friend Requests I
```
| sender_id | send_to_id |request_date|
|-----------|------------|------------|
| 1         | 2          | 2016_06-01 |
| 1         | 3          | 2016_06-01 |
| 1         | 4          | 2016_06-01 |
| 2         | 3          | 2016_06-02 |
| 3         | 4          | 2016-06-09 |
Table: request_accepted
| requester_id | accepter_id |accept_date |
|--------------|-------------|------------|
| 1            | 2           | 2016_06-03 |
| 1            | 3           | 2016-06-08 |
| 2            | 3           | 2016-06-08 |
| 3            | 4           | 2016-06-09 |
| 3            | 4           | 2016-06-10 |
```
Write a SQL query that finds the overall acceptance rate of requests, rounded to 2 decimals. The acceptance rate is the number of acceptances divided by the number of requests. It is possible for multiple requests to the same receiver to be sent and requests to be accepted more than once; in these cases the requests and acceptances should only be counted once. If there are no requests, return 0.00 as the acceptance rate.
```
|accept_rate|
|-----------|
|       0.80|
```
Source: LC 597

Solution:
```SQL
select round(
  ifnull(
    (select count(*) from (select distinct requester_id, accepter_id from requested_accepted) as a)
    /
    (select count(*) from (select distinct sender_id, send_to_id from friend_request) as b)
  , 0)
, 2) as accept_rate;
```
#### 1.4 Consecutive Numbers
```
Table: Logs
+----+-----+
| Id | Num |
+----+-----+
| 1  |  1  |
| 2  |  1  |
| 3  |  1  |
| 4  |  2  |
| 5  |  1  |
| 6  |  2  |
| 7  |  2  |
+----+-----+
```
Write a SQL query that finds all numbers taht appear in `Logs` at least three times consecutively.
```
+-----------------+
| ConsecutiveNums |
+-----------------+
| 1               |
+-----------------+
```
Source: LC 180

Solution:
```SQL
select distinct a.Num as ConsecutiveNums
from logs as a, logs as b, logs as c
where a.num = b.num
and b.num = c.num
and a.Id = b.Id + 1
and b.Id = c.Id + 1;
```
#### 1.5
#### 1.6
#### 1.7
#### 1.8
