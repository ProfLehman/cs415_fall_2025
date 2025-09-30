# CS415 – Join Practice

## Tables

Create the following tables in your database.

### student
| sid | name  |
|-----|-------|
|  1  | Alice |
|  2  | Bob   |
|  3  | Carol |
|  4  | Dan   |
|  5  | Erin  |

### enrollment
| eid | sid | course   |
|-----|-----|----------|
| 101 |  1  | Math     |
| 102 |  1  | CS       |
| 103 |  3  | History  |
| 104 |  5  | Biology  |
| 105 |  6  | Math     |   -- sid=6 does not exist in student

---
## Create sample tables

```sql
CREATE TABLE student (
   sid INT PRIMARY KEY,
   name VARCHAR(20)
);

INSERT INTO student VALUES
(1, 'Alice'),
(2, 'Bob'),
(3, 'Carol'),
(4, 'Dan'),
(5, 'Erin');

CREATE TABLE enrollment (
   eid INT PRIMARY KEY,
   sid INT,
   course VARCHAR(20)
);

INSERT INTO enrollment VALUES
(101, 1, 'Math'),
(102, 1, 'CS'),
(103, 3, 'History'),
(104, 5, 'Biology'),
(105, 6, 'Math'); 

```
## Remove tables

Run the following to remove the tables from your database;

```sql
drop table enrollment;

drop table student;
```
---
## Questions

1. Show all students who are enrolled in at least one course (**INNER JOIN**).
2. Show all students and their courses (**LEFT JOIN**). If no course, show NULL.
3. Show all enrollments and match them to student names (**RIGHT JOIN**). If no student, show NULL.
4. Show all students and all enrollments (**FULL OUTER JOIN**).
5. List the students who are not enrolled in any course.

   | sid | name |
   |-----|------|
   |  2  | Bob  |
   |  4  | Dan  |

6. List the invalid enrollments (enrollments that do not have a matching student).

   | eid | sid | course |
   |-----|-----|--------|
   | 105 |  6  | Math   |

---

## CS415 – Join Practice (Answer Key)

### 1. INNER JOIN
```sql
SELECT s.sid, s.name, e.course
FROM student s
INNER JOIN enrollment e
  ON s.sid = e.sid;
````

### 2. LEFT JOIN

```sql
SELECT s.sid, s.name, e.course
FROM student s
LEFT JOIN enrollment e
  ON s.sid = e.sid;
```

### 3. RIGHT JOIN

```sql
SELECT s.sid, s.name, e.course
FROM student s
RIGHT JOIN enrollment e
  ON s.sid = e.sid;
```

### 4. FULL OUTER JOIN (MariaDB/MySQL)

```sql
SELECT s.sid, s.name, e.course
FROM student s
LEFT JOIN enrollment e
  ON s.sid = e.sid
UNION
SELECT s.sid, s.name, e.course
FROM student s
RIGHT JOIN enrollment e
  ON s.sid = e.sid;
```

### 5. Students NOT Enrolled

```sql
SELECT s.sid, s.name
FROM student s
LEFT JOIN enrollment e
  ON s.sid = e.sid
WHERE e.sid IS NULL;
```

### 6. Invalid Enrollments

```sql
SELECT e.eid, e.sid, e.course
FROM enrollment e
LEFT JOIN student s
  ON e.sid = s.sid
WHERE s.sid IS NULL;
```

-- end --

