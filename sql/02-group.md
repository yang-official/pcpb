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

#### 2.2
