## Basic Commands

### INPUT
```
show databases;
```
### OUTPUT
```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.070 sec)
```
To see all the available databases in the system

---

### INPUT
```
create database <db-name>;
```
```
create database demo;
```
### OUTPUT
```
Query OK, 1 row affected (0.089 sec)
```
To create the new database in the system

---

### INPUT
```
use <db-name>;
```
```
use demo;
```
### OUTPUT
```
Database changed
```
To switch to the perticular databse

---

### INPUT
```
create table <table-name>(schema);
```
```
create table users (
    id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(20),
    password VARCHAR(40),
    joined DATE
);
```
### OUTPUT
```
Query OK, 0 rows affected (0.327 sec)
```
To create a table in current database

---

### INPUT
```
desc <table-name>;
```
```
desc users;
```
### OUTPUT
```
+----------+-------------+------+-----+---------+----------------+
| Field    | Type        | Null | Key | Default | Extra          |
+----------+-------------+------+-----+---------+----------------+
| id       | int         | NO   | PRI | NULL    | auto_increment |
| username | varchar(20) | YES  |     | NULL    |                |
| password | varchar(40) | YES  |     | NULL    |                |
| joined   | date        | YES  |     | NULL    |                |
+----------+-------------+------+-----+---------+----------------+
4 rows in set (0.001 sec)
```
To see the shcema of perticular table


---
## CURD Operations

### INPUT
```
insert into <table-name>(coloumn-names...)values(coloumn-values...);
```
```
inser into users (
    id,
    username,
    password
) values (
    3,
    'abuzark',
    'veryseceret'
);
```
### OUTPUT
```
Query OK, 1 row affected (0.166 sec)
```
To insert the row of data for specific columns into the perticular table (safe)

---

### INPUT
```
insert into <table-name> values(coloumn-values...);
```
```
insert into users values (
    6,
    'kira'
    'deathnote',
    '2006-10-04'
);
```
### OUTPUT
```
Query OK, 1 row affected (0.073 sec)
```
To insert the row of data for all the coloumns into the perticular table (unsafe)

---

### INPUT
```
select <coloumn-names> from <table-name>;
```
```
select * from users;
```
### OUTPUT
```
+----+----------+------------+------------+
| id | username | password   | joined     |
+----+----------+------------+------------+
|  5 | abuzark  | verysecure | NULL       |
|  6 | kira     | deathnote  | 2006-10-04 |
+----+----------+------------+------------+
2 rows in set (0.000 sec)
```
To view the data of specific coloumns from a perticular table 

---

### INPUT
```
select <coloumn-names> from <table-name> order by <coloumn-name> <order>;
```
```
select * from users order by joined asc;
```
### OUTPUT
```
+----+----------+------------+------------+
| id | username | password   | joined     |
+----+----------+------------+------------+
|  6 | kira     | deathnote  | 2006-10-04 |
|  5 | abuzark  | verysecure | 2025-10-06 |
+----+----------+------------+------------+
2 rows in set (0.000 sec)
```
To view all the rows ordered by specific coloumn from a perticular table 

---

### INPUT
```
select <coloumn-names> from <table-name> where <condition>;
```
```
select * from users where username='kira';
```
### OUTPUT
```
+----+----------+-----------+------------+
| id | username | password  | joined     |
+----+----------+-----------+------------+
|  6 | kira     | deathnote | 2006-10-04 |
+----+----------+-----------+------------+
1 row in set (0.000 sec)
```
To view all the rows from a perticular table where given condition is satisfied 

---

### INPUT
```
select <coloumn-names> from <table-name> where <coloumn-name> like <value>;
```
```
select * from users where username like 'k%;
```
### OUTPUT
```
+----+----------+-----------+------------+
| id | username | password  | joined     |
+----+----------+-----------+------------+
|  6 | kira     | deathnote | 2006-10-04 |
+----+----------+-----------+------------+
1 row in set (0.000 sec)
```
To view all the rows from a perticular table where the value of specific coloumn starts with given character

> **%** is wildcard character and **_** is a place holder when used with **like** operator.

- (**s%**) all the values starts with **s** and are indefinite character long

- (**%k**) all the values ends with **k** and are indifinite character long

- (**a_____**) all the values starts with **a** and are **6** character long

- (**%r_**) all the values whos second last character is **r** and are indifinite characters long

---

### INPUT
```
update <table-name> set <column-names>=<new-value> where <condition>
```
```
update users set joined='2025-10-05' where id=5;
```
### OUTPUT
```
Query OK, 1 row affected (0.060 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```
To update the value of specific coloumns in a perticular table

---

### INPUT
```
alter table <table-name> add <coloumn-name> <coloumn-type>;
```
```
alter table users add role varchar(10);
```
### OUTPUT
```
Query OK, 0 rows affected (0.170 sec)
Records: 0  Duplicates: 0  Warnings: 0
```
To add a new coloumn into the perticular table

---

### INPUT
```
alter table <table-name> modify column <coloumn-name> <modification>;
```
```
alter table users modify column username varchar(30);
```
### OUTPUT
```
Query OK, 0 rows affected (0.079 sec)
Records: 0  Duplicates: 0  Warnings: 0
```
To modify the speicific coloumn from the perticular table

---

### INPUT
```
alter table <table-name> drop column <coloumn-name>;
```
```
alter table users drop column role;
```
### OUTPUT
```
Query OK, 0 rows affected (0.156 sec)
Records: 0  Duplicates: 0  Warnings: 0
```
To remove the specific coloumn from the perticular table

---

### INPUT 
```
delete from <table-name> where <condition>;
```
```
delete from users where username='kira';
```
### OUTPUT
```
Query OK, 1 row affected (0.066 sec)
```
To delete the specific row from a perticular table

---

## Table Joins

### INPUT
```
select <coloumn-name> from <table-name(1)> inner join <table-name(2)> on <table-name(1)>.<coloumn-name>=<table-name(2)>.<coloumn-name>;
```
```
select employees_us.first_name, employees_us.salary, employees_uk.first_name, employees_uk.salary from employees_us inner join employees_uk on employees_us.salary=employees_uk.salary;
```
### OUTPUT
```
+------------+----------+------------+----------+
| first_name | salary   | first_name | salary   |
+------------+----------+------------+----------+
| Bob        | 60000.00 | Anna       | 60000.00 |
+------------+----------+------------+----------+
| Robert     | 60000.00 | Alice      | 60000.00 |
+------------+----------+------------+----------+
2 row in set (0.000 sec)
```
To joing the two tables together on perticular field where the value are same in both table

---

### INPUT
```
select <coloumn-name> from <table-name(1)> right join <table-name(2)> on <table-name(1)>.<coloumn-name>=<table-name(2)>.<coloumn-name>;
```
```
select employees_us.emp_id, employees_us.first_name, employees_uk.emp_id, employees_uk.first_name from employees_us right join employees_uk on employees_us.emp_id=employees_uk.emp_id;
```
### OUTPUT
```
+--------+------------+--------+------------+
| emp_id | first_name | emp_id | first_name |
+--------+------------+--------+------------+
|      1 | Alice      |      1 | Emily      |
|   NULL | NULL       |      2 | Frank      |
|      3 | Carol      |      3 | Grace      |
|      4 | David      |      4 | Bob        |
+--------+------------+--------+------------+
4 rows in set (0.000 sec)
```
To joing the two tables on perticular field where if the field value does not match the row on right table gonna show **NULL** 

---

### INPUT
```
select <coloumn-name> from <table-name(1)> cross join <table-name(2)>;
```
```
select employees_us.emp_id, employees_us.first_name, employees_uk.emp_id, employees_uk.first_name from employees_uk cross join employees_us;
```
### OUTPUT
```
+--------+------------+--------+------------+
| emp_id | first_name | emp_id | first_name |
+--------+------------+--------+------------+
|      1 | Alice      |      4 | Bob        |
|      1 | Alice      |      3 | Grace      |
|      1 | Alice      |      2 | Frank      |
|      1 | Alice      |      1 | Emily      |
|      2 | Bob        |      4 | Bob        |
|      2 | Bob        |      3 | Grace      |
|      2 | Bob        |      2 | Frank      |
|      2 | Bob        |      1 | Emily      |
|      3 | Carol      |      4 | Bob        |
|      3 | Carol      |      3 | Grace      |
|      3 | Carol      |      2 | Frank      |
|      3 | Carol      |      1 | Emily      |
|      4 | David      |      4 | Bob        |
|      4 | David      |      3 | Grace      |
|      4 | David      |      2 | Frank      |
|      4 | David      |      1 | Emily      |
+--------+------------+--------+------------+
16 rows in set (0.000 sec)
```
To join two tables where each individual row from the first table joins with every row single row from second table producing all the possible combinations

---

### INPUT
```
select <coloumn-name> from <table-name> union select <coloumn-name> from <table-name>
```
```
select emp_id, first_name, last_name from employees_us union select emp_id, first_name, last_name from employees_uk;
```
### OUTPUT
```
+--------+------------+-----------+
| emp_id | first_name | last_name |
+--------+------------+-----------+
|      1 | Alice      | Johnson   |
|      2 | Bob        | Smith     |
|      3 | Carol      | Davis     |
|      4 | David      | White     |
|      1 | Emily      | Brown     |
|      2 | Frank      | Wilson    |
|      3 | Grace      | Taylor    |
|      4 | Bob        | Smith     |
+--------+------------+-----------+
8 rows in set (0.000 sec)
```
To merge two tables data into one big table

> the field type and number of coloumns must match

---

## Inbuilt Funtions

**`sum(coloumn-name)`** -> gives the sum of value of specific coloumn for all the rows

### INPUT
```
select sum(price) from cart;
```
### OUTPUT
```
+---------------+
| sum(cart)     |
+---------------+
|       150,800 |
+---------------+
```
---

**`avg(coloumn-name)`** -> gives the average of value of specific coloumn for all the rows

### INPUT
```
select avg(age) from customer;
```
### OUTPUT
```
+---------------+
| avg(age)      |
+---------------+
|        27.333 | 
+---------------+
```

---

**`count(column-name)`** -> gives the total number of rows has the data filled for given coloumn

### INPUT
```
select count(username) from users;
```
### OUTPUT
```
+-----------------+
| count(username) |
+-----------------+
|            3022 |
+-----------------+
```

---

**`min(coloumn-name)`** -> returns the row which has the lowest value in speicific coloumn

### INPUT
```
select min(age) from customer;
```
### OUTPUT
```
+---------------+
| min(age)      |
+---------------+
|            17 | 
+---------------+
```

---

**`max(coloumn-name)`** -> returns the row which has the highest value in speicific coloumn

### INPUT
```
select min(age) from customer;
```
### OUTPUT
```
+---------------+
| max(age)      |
+---------------+
|            71 | 
+---------------+
```

---