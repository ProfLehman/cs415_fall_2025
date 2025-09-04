## Practice Exercises #1 - In-Class
- CS 415 Database Management
- Fall 2025  
- MariaDB Essential Commands
- DB-02, SQL-01

---
## MariaDB Web Client
Use **phpMyAdmin** to connect to the MariaDB server hosted on `ada.huntington.edu`.
phpMyAdmin is a web client interface to the database.

- **Username**: your last name (all lowercase)
- Example: `smith`  
- **Password**: Ask Prof. Lehman

[Click  here for phpMyAdmin on Ada](https://ada.huntington.edu/phpmyadmin/)

In phpMyAdmin, click the **SQL** tab, enter commands, and press **Go**.

---
## See database version
```sql
select version();
````

## See available databases

```sql
show databases;
```

## Select a database

```sql
use demo;
```

## List tables in the database

```sql
show tables;
```

## See table structure

```sql
describe student;
desc student;
show columns from student;
show create table student;
```

## Show all data in table format

```sql
select * from student;
```

## Limit results (first X rows)

```sql
select * from student limit 5;
```

## Choose specific columns

```sql
select first_name, last_name from student;
```

---

## Change your database account password

```sql
set password = password("new_password");
```

## See users and passwords (usually only available to admin account)

```sql
use mysql;
select user, host, password from user;
```

---

## Logout

In phpMyAdmin, click the **Logout** button (to the right of the Home button).

--- end ---

