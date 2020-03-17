# Chapter 2: Group

#### 2.1 Duplicate Emails
```
Table: Person
+----+---------+
| Id | Email   |
+----+---------+
| 1  | a@b.com |
| 2  | c@d.com |
| 3  | a@b.com |
+----+---------+
```
Given the above table `Person`, write a SQL query that finds all the duplicate emails.
```
+---------+
| Email   |
+---------+
| a@b.com |
+---------+
```
Source: LC 182

Solution:
```SQL
select Email from Person
group by Email
having count(Email) > 1;
```

#### 2.2 Delete Duplicate Emails
```
Table: Person, primary key: Id
+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |
+----+------------------+
```
Given the table `Person`, write a SQL query that deletes all duplicate email entries, keeping only unique emails based on the smallest Id. The output is the `Person` table itself. Use the `delete` statement.
```
+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
+----+------------------+
```
Source: LC 196

Solution:
```SQL
select min(Id) as minId, Email from Person group by Email;
delete from Person where Id not in (
  select minId from (
    select min(Id) as minId, Email from Person group by Email
  ) as tmp
);
```

#### 2.3 Game Play Analysis I


#### 2.4 Game Play Analysis II
#### 2.5 Trips and Users
#### 2.6 Managers with at least 5 direct reports
