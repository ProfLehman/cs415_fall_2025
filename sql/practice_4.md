# In-Class Lab - Pets
#

## In-Class Lab For this lab, use the pet table below from the demo database

Note: ** see solutions below **

1. How can you see all the tables in the demo database?

2. Display the structure of the pets table (field names and data types)

3. Show all columns and rows from the pets table sorted oldest to youngest by birthday.

4. List the names and species of the first 5 pets.

5. Find all pets that live in the city of “Fort Wayne.”

6. List all pets whose names start with the letter “B.”

7. Show all pets that are either cats or dogs.

8. Find pets with birthdays in the year 2020.

9. List pets with ages between 3 and 7 years old.

10.  List all of the species of pets (each species listed one time).

```SQL
+-------+---------+---------+--------------------+------+---------------+--------------+------------+
| petid | name    | species | breed              | age  | owner         | city         | birthday   |
+-------+---------+---------+--------------------+------+---------------+--------------+------------+
|     1 | Bella   | Dog     | Labrador Retriever |    5 | Alice Johnson | Huntington   | 2019-06-12 |
|     2 | Max     | Dog     | German Shepherd    |    7 | Brian Smith   | Fort Wayne   | 2017-03-08 |
|     3 | Luna    | Cat     | Siamese            |    3 | Cathy Brown   | Indianapolis | 2021-11-20 |
|     4 | Charlie | Dog     | Beagle             |    4 | David Wilson  | Huntington   | 2020-09-15 |
|     5 | Daisy   | Rabbit  | Holland Lop        |    2 | Emily Davis   | Fort Wayne   | 2022-05-02 |
|     6 | Oliver  | Cat     | Maine Coon         |    6 | Frank Miller  | South Bend   | 2018-07-25 |
|     7 | Milo    | Dog     | Bulldog            |    1 | Grace Lee     | Huntington   | 2023-01-05 |
|     8 | Coco    | Bird    | Parakeet           |    2 | Henry Clark   | Bloomington  | 2022-02-14 |
|     9 | Ruby    | Cat     | Persian            |    4 | Isla Martinez | Fort Wayne   | 2020-12-30 |
|    10 | Rocky   | Dog     | Boxer              |    8 | Jack Thompson | Huntington   | 2016-04-10 |
|    11 | Nala    | Cat     | Bengal             |    5 | Karen White   | Indianapolis | 2019-08-09 |
|    12 | Buddy   | Dog     | Golden Retriever   |    6 | Liam Harris   | Huntington   | 2018-10-22 |
|    13 | Rosie   | Rabbit  | Mini Rex           |    3 | Mia Young     | Fort Wayne   | 2021-04-18 |
|    14 | Chloe   | Cat     | Ragdoll            |    2 | Noah Walker   | Huntington   | 2022-09-02 |
|    15 | Leo     | Dog     | Poodle             |    7 | Olivia Allen  | South Bend   | 2017-12-11 |
|    16 | Mango   | Bird    | Cockatiel          |    1 | Paul Scott    | Indianapolis | 2023-06-01 |
|    17 | Zoe     | Cat     | Sphynx             |    5 | Quinn Adams   | Fort Wayne   | 2019-02-27 |
|    18 | Finn    | Dog     | Dachshund          |    4 | Rachel Baker  | Huntington   | 2020-11-19 |
|    19 | Willow  | Rabbit  | English Angora     |    6 | Sam Carter    | Bloomington  | 2018-03-07 |
|    20 | Sunny   | Bird    | Canary             |    3 | Tina Evans    | Fort Wayne   | 2021-07-16 |
+-------+---------+---------+--------------------+------+---------------+--------------+------------+
```
---

## Sample Solutions
Here you go—each item states the question and shows the SQL using your `pets` table (columns: `petid, name, species, breed, age, owner, city, birthday`).

> Tip: if needed, select the database first:

```sql
USE demo;
```

---

### 1) How can you see all the tables in the `demo` database?

```sql
SHOW TABLES;

-- or, explicitly:
SHOW TABLES FROM demo;
```

---

### 2) Display the structure of the `pets` table (field names and data types)

```sql
DESCRIBE pets;
-- equivalents:
DESC pets;
SHOW COLUMNS FROM pets;
```

---

### 3) Show all columns and rows from the `pets` table sorted oldest to youngest by `birthday`

```sql
SELECT *
FROM pets
ORDER BY birthday ASC;   -- oldest (earliest date) first
```

---

### 4) List the `name` and `species` of the first 5 pets

```sql
SELECT name, species
FROM pets
ORDER BY petid
LIMIT 5;
```

---

### 5) Find all pets that live in the city of “Fort Wayne”

```sql
SELECT *
FROM pets
WHERE city = 'Fort Wayne';
```

---

### 6) List all pets whose names start with the letter “B”

```sql
SELECT *
FROM pets
WHERE name LIKE 'B%';
```

---

### 7) Show all pets that are either cats or dogs

```sql
SELECT *
FROM pets
WHERE species IN ('Cat', 'Dog');

-- alternate approach
SELECT *
FROM pets
WHERE species = "Cat" or species = "Dog");

```

---

### 8) Find pets with birthdays in the year 2020

```sql
-- Option A: using YEAR()
SELECT *
FROM pets
WHERE YEAR(birthday) = 2020;

-- alternate
SELECT *
FROM pets
WHERE birthday >= '2020-01-01'
  AND birthday <  '2021-01-01';

-- alternate
SELECT *
FROM pets
WHERE birthday BETWEEN '2020-01-01'
  AND '2021-01-01';
 
  
```

---

### 9) List pets with ages between 3 and 7 years old

```sql
SELECT *
FROM pets
WHERE age BETWEEN 3 AND 7;   -- inclusive of 3 and 7

-- alternate
SELECT *
FROM pets
WHERE age >= 3 AND age <= 7;   -- inclusive of 3 and 7

```

---

### 10) List all of the species of pets (each species listed one time)

```sql
SELECT DISTINCT species
FROM pets
ORDER BY species;
```

-- end --
