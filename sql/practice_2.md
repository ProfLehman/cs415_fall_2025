# Practice Exercises #2 – In-Class  
- CS415 Database Management
- Fall 2025  
- DB-02, SQL-01, SQL-02

---

## Database Basics

```sql
-- see database version
select version();

-- change database password (in MariaDB)
set password = password("new_password");

-- show databases available to user
show databases;

-- select database
use university;

-- see tables in the selected database
show tables;

-- see table structure
-- note PRI indicates a primary key
describe course;    
desc course;
show columns from course;
````

---

## Viewing Data

```sql
-- show all data and rows from the table
select * from course;

-- show data in one column format (command line)
select * from student\G

-- use limit to show the first X rows
select * from course limit 5;
```

---

## Calculator & Functions

```sql
-- use as a calculator
select 7 - 2 * 3;

-- use functions
select abs(-3);
```

---

## Selecting Columns

```sql
-- select multiple fields
select cid, name from course limit 3;

select cid, hours, fee 
from course;

-- rename columns for readability
SELECT 
  cid as "Course", 
  hours as "Hours",
  fee as "Student Cost" 
FROM course;

-- same query in one line
SELECT cid as "Course", hours as "Hours", fee as "Student Cost" FROM course;
```

---

## Calculated Fields

```sql
-- calculated fields
select 
  cid, 
  hours, 
  fee, 
  fee * .9 as "new fee",
  fee - 5 as "other option"
from course 
limit 5;

-- proposed fee increase
select 
  cid, 
  hours, 
  fee as "Current",
  fee * 1.15 as "Proposed"
from course;

-- alternate calculation
select 
  cid, 
  hours, 
  fee as "Current",
  fee + (fee * .15) as "Proposed"
from course;

-- rounding
select 
  cid, 
  hours, 
  fee as "Current",
  round(fee + (fee * .15), 2) as "Proposed"
from course;
```

---

## Functions on Fields

```sql
-- square root of fee
select fee, sqrt(fee) from course;

-- random number * fee
select round(rand() * fee, 0) from course;

-- random 1–5 rating per student
select last, round(rand()*5,0)+1 from student;
```

---

## Sorting Results

```sql
-- sort ascending gender (ASC is default)
select first, gender 
from student 
order by gender;

-- explicit ASC
select first, gender 
from student 
order by gender ASC;

-- descending gender
select first, gender 
from student 
order by gender DESC;

-- descending gender, ascending first
select gender, first 
from student 
order by gender DESC, first;

-- ascending gender, ascending first
select gender, first 
from student 
order by gender, first;

-- ascending gender, descending first
select gender, first 
from student 
order by gender, first DESC;
```

---

## DISTINCT

```sql
-- all cities with duplicates
select city from student;

-- remove duplicates
select distinct city from student;
```

---

## Filtering Rows with WHERE

```sql
select cid, hours
from course
where cid = 3;

select last, city, state 
from student 
where city = "Huntington";

select last, city, state 
from student 
where state = "OH";

select last, city, state 
from student 
where state = "OH" or city = "Huntington";

select last, city, state 
from student 
where state = "OH" and city = "Huntington";

select last, city, state, gender  
from student  
where state = "IN" 
  and gender = "m";

select last, city, state, gender 
from student 
where gender = "f" and city = "Huntington";

select last, city, state, gender 
from student 
where gender = "f" or city = "Huntington";

SELECT cid, hours
FROM course
WHERE hours = 4;

SELECT cid, hours
FROM course
WHERE hours = 4 or hours = 3;

SELECT cid, hours
FROM course
WHERE hours = 4 or hours = 3
ORDER BY hours;
```

---

## LIKE Patterns

```sql
-- city starts with s
select city
from student
where city like "s%";

-- city ends with s
select city
from student
where city like "%s";

-- city has an s anywhere
select city
from student
where city like "%s%";
```

--- end ---
