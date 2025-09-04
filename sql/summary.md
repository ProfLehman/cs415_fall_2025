## Practice Exercises #3 - Command Formats
- CS 415 Database Management - Fall 2025
- DB-02, SQL-01, SQL-02

---
```sql
-- distinct
select distinct field from table;
select distinct field1, field2 from table;

-- exact match
select field from table where field = "value";
select field from table where field like "value";

-- pattern match
select field from table where field like "%suffix";   -- ends with
select field from table where field like "prefix%";   -- starts with
select field from table where field like "_o%";       -- second letter o
select field from table where field like "%text%";    -- contains text
select field from table where field not like "___234%"; -- exclude pattern

-- IN, NOT IN
select fields from table where field in ("value1", "value2", ...);
select fields from table where field not in ("value1", "value2", ...);

-- BETWEEN operator
select fields from table where field >= low and field <= high;
select fields from table where field between low and high;

-- case conversion
select upper(field), lower(field) from table;

-- concatenation
select concat(f1, " ", f2) as fullname from table;
select concat_ws(",", f1, f2, f3) from table;

-- substrings
select left("text", n);
select right("text", n);
select mid("text", start, length);
select email, instr(email,"@") from member;
select email, mid(email, instr(email,"@")+1, 200) as host from member;

--date and time
select now(), curdate(), curtime();
select year(date), month(date), monthname(date) from table;
select * from table where year(date) = 1993;
select * from table where date between "1993-01-01" and "1993-12-31";
select * from table where month(date) between 7 and 8 and year(date) = 1993;
select birthday, timestampdiff(year, birthday, "2023-08-29") as age from student;

-- number bases
select bin(10), oct(10), hex(10);
```
--- end ---


```
