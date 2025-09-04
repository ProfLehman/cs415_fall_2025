## Practice Exercises #3 - In-Class
- CS 415 Database Management
- DB-02, SQL-01, SQL-02

---

## DISTINCT
Adding `distinct` removes duplicate **rows** (not just duplicates in the first column).

```sql
-- distinct values for hours
select distinct hours from course;

-- distinct values for fee
select distinct fee from course;

-- distinct fee and hour combinations
select distinct fee, hours from course;
````

---

## LIKE and Wildcards

* `=` and `LIKE` behave the same for exact matches.
* `%` matches zero or more characters.
* `_` matches exactly one character.

```sql
-- exact match
select city from student where city = "Huntington";

-- exact match
select city from student where city like "Huntington";

-- end with "ton"
select city from student where city like "%ton";

-- this does NOT work, must use like
select city from student where city = "%ton";

-- contains "n"
select city from student where city like "%n%";

-- ends with "n"
select city from student where city like "%n";

-- starts with "n"
select city from student where city like "n%";

-- starts with "h" and ends with "n"
select city from student where city like "h%n";

-- contains "on"
select city from student where city like "%on%";

-- second letter is "o"
select city from student where city like "_o%";

-- phone with prefix 234
select phone from student where phone like "___234%";

-- phone NOT starting with 234 after 3 digits
select phone from student where phone not like "___234%";
```

---

## IN and BETWEEN

### IN operator

Shorthand for multiple `OR` conditions.

```sql
select last, state 
from student 
where state in ("IL","IN");

select last, state 
from student 
where state not in ("IL","IN","MI");
```

### BETWEEN operator

Shorthand for inclusive ranges.

```sql
select last 
from student 
where last between "Davis" and "Ming"
order by last;
```

---

## String and Text Functions

### Case Conversion

```sql
select upper(last), lower(last) from student;
```

### Concatenation

```sql
-- simple concat
select concat(first, " ", last) as fullname 
from student;

-- concat with separator
select concat_ws(",", first, last, title, city) 
from member;
```

### Substrings

```sql
select left("sample", 2);   -- "sa"
select right("sample", 2);  -- "le"
select mid("sample", 2, 3); -- "amp"
```

### Example: Initial Code

```sql
select last, 
   ucase(concat(left(last,1), right(last,1))) as code
from member limit 10;
```

### Email Host Example

```sql
select email, instr(email, "@") 
from member;

select email,
   mid(email, instr(email,"@")+1, 200) as host
from member;
```

---

## Date and Time Functions

### Current Date/Time

```sql
select now();      -- current date & time
select curdate();  -- current date
select curtime();  -- current time
```

### Birthdays

```sql
-- show date parts
select birthday, year(birthday), month(birthday), monthname(birthday)
from student;

-- students born in 1993
select birthday 
from student 
where year(birthday) = 1993;

-- alternative approaches
select birthday from student where birthday like "1993%";
select birthday from student where birthday between "1993-01-01" and "1993-12-31";
```

### Birth Month Example

```sql
select birthday
from student
where month(birthday) between 7 and 8
  and year(birthday) = 1993;
```

### Age Calculation

```sql
select birthday, 
   timestampdiff(year, birthday, "2023-08-29") as age
from student;
```

---

## Numeric/Conversion Functions

```sql
select bin(10), oct(10), hex(10);
```

-- end --
