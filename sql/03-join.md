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

#### 3.2 Employees Earning More than their Managers

Source: LC 181
