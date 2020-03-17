# Chapter 3: Joins

#### 3.1 Combine Two Tables
```
Table: Person, primary key: PersonId
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| PersonId    | int     |
| FirstName   | varchar |
| LastName    | varchar |
+-------------+---------+
Table: Address, primary key: AddressId
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| AddressId   | int     |
| PersonId    | int     |
| City        | varchar |
| State       | varchar |
+-------------+---------+
```
Write a SQL query that provides the following information for each person in the `Person` table, regardless of if there is an address:
`FirstName, LastName, City, State`

Source: LC 175

Solution
```SQL
select FirstName, LastName, City, State
from Person left join Address
on Person.PersonId = Address.PersonId;
```
#### 3.2 Customers who Never Order
```
Table: Customers.
+----+-------+
| Id | Name  |
+----+-------+
| 1  | Joe   |
| 2  | Henry |
| 3  | Sam   |
| 4  | Max   |
+----+-------+
Table: Orders.
+----+------------+
| Id | CustomerId |
+----+------------+
| 1  | 3          |
| 2  | 1          |
+----+------------+
```
Given the `Customers` and `Orders` tables, write a SQL query that finds all customers who never order:
```
+-----------+
| Customers |
+-----------+
| Henry     |
| Max       |
+-----------+
```
Source: LC 183

Solution
```SQL
select Name as Customers
from customers c left join orders o
on c.Id = o.CustomerId
where o.CustomerId is null;
```

#### 3.3 Employees Earning More than their Managers
```
Table: Employee
+----+-------+--------+-----------+
| Id | Name  | Salary | ManagerId |
+----+-------+--------+-----------+
| 1  | Joe   | 70000  | 3         |
| 2  | Henry | 80000  | 4         |
| 3  | Sam   | 60000  | NULL      |
| 4  | Max   | 90000  | NULL      |
+----+-------+--------+-----------+
```
Given the `Employee` table, write a SQL query that finds all employees who earn more than their managers:
```
+----------+
| Employee |
+----------+
| Joe      |
+----------+
```
Source: LC 181

Solution
```SQL
select Name as Employee
from Employee e join Employee m
on e.ManagerId = m.Id
where e.Salary > m.Salary;
```
