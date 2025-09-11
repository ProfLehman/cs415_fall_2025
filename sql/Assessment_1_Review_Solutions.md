## Assessment 1 Review - Sample SQL Solutions

---

### 1. Update the current user password to be "exam1secret"

```sql
SET PASSWORD = PASSWORD('exam1secret');
```

### 2. Display a list of all databases available

```sql
SHOW DATABASES;
```

### 3. Choose the database called "demo" and display all tables from this database

```sql
USE demo;
SHOW TABLES;
```

### 4. Display the table structure information (fields, field types, keys) for the table called "member"

```sql
DESCRIBE member;
DESC member;
SHOW COLUMNS FROM member;
```

### 5. Display all columns and rows from the table "member"

```sql
SELECT * FROM member;
```

### 6. Display all columns and the first two rows from the table "member"

```sql
SELECT * FROM member
LIMIT 2;
```

To get last two rows use 

```sql
SELECT * FROM member
ORDER BY mid DESC
LIMIT 2;
```


---

### 7. Display the last name and state for all records in the member table

```sql
SELECT last, state
FROM member;
```

### 8. Display the last name and state for all records in the member table, sorted by ascending last name

```sql
SELECT last, state
FROM member
ORDER BY last ASC;
```

### 9. Display the last name and birthday for all records in the member table, sorted by descending birthday and ascending last name

```sql
SELECT last, birthdate
FROM member
ORDER BY birthdate DESC, last ASC;
```

Note: Sorting happens by the first field, then if there are duplicates
with the first field, the second is used.  If there are no duplicates
with the first field, the second has no affect

```sql
select state, last
from member
order by state, last;

select state, last
from member
order by state, last DESC;
```

---

### 10. Display all projects that have the letters “er” in the project name

```sql
SELECT *
FROM project
WHERE name LIKE '%er%';
```

### 11. Display all donations made in August of any year

```sql
SELECT *
FROM donation
WHERE MONTH(received) = 8;

-- alternate approach, not recommended as dates are stored differently
SELECT *
FROM donation
WHERE received like "%-08-%";

```

### 12. Display all donations made in August or April

```sql
SELECT *
FROM donation
WHERE MONTH(received) = 8 or MONTH(received) = 4;

-- alternate approach with IN
SELECT *
FROM donation
WHERE MONTH(received) IN (8, 4);
```

### 13. Display all donation amounts and create a calculated column that shows the donation plus 10%

```sql
SELECT amount,
       amount * 1.10 AS amount_plus_10pct
FROM donation;
```

---

### 14. Display all donations made during the time period 8-1-2023 to 8-15-2023

```sql
SELECT *
FROM donation
WHERE received BETWEEN '2023-08-01' AND '2023-08-15';

-- alternate approach
SELECT *
FROM donation
WHERE received >= "2023-08-01" AND received <= "2023-08-15";
 
```

### 15. Display a list of all states from members, removing the duplicates

```sql
SELECT DISTINCT state
FROM member
ORDER BY state;
```

### 16. Display the state for each member

```sql
SELECT state
FROM member;
```

### 17. Display the state and number of members in each state

```sql
SELECT state, COUNT(*) AS member_count
FROM member
GROUP BY state
ORDER BY member_count DESC, state;
```

### 18. Display the state and number of members in each state that has 3 or more members

```sql
SELECT state, COUNT(*) AS member_count
FROM member
GROUP BY state
HAVING COUNT(*) >= 3
ORDER BY member_count DESC, state;
```

### 19. Generate a greeting for each member in the format “Dear Alice Anderson,”

```sql
SELECT CONCAT('Dear ', first, ' ', last, ',') AS greeting
FROM member;
```

### 20. List all members using Last, First format (e.g., Smith, John) sorted by last and first name ascending

```sql
SELECT CONCAT(last, ', ', first) AS name
FROM member
ORDER BY last ASC, first ASC;
```

### 21. Generate a standard user login using the first initial and last name (e.g., NForester for Norman Forester)

```sql
SELECT CONCAT(
         LEFT(first, 1),
         last
       ) AS user_login
FROM member;
```

-- end --
