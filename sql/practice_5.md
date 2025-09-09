## Practice Exercises #5 - Aggregations
- CS 415 Database Management
- Fall 2025
- SQL-03 Aggregations

---

## Aggregations
Aggregations in SQL are operations that combine values from multiple rows into a single summary value. 
Common aggregation functions include `COUNT`, `SUM`, `AVG`, `MIN`, and `MAX`. 

These aggregations are often paired with `GROUP BY` to organize results into categories and `HAVING` to restrinct rows.

They are especially useful for analyzing data trends, producing summaries, and supporting decision-making from large datasets.


## use demo database with pets table for these examples
```sql
use demo;
select * from pets;
```

---

## Aggregations applied to the entire table

### 1. Total number of pets
```sql
select count(*) as total_pets from pets;
```

### 2. Average age of all pets
```sql
select avg(age) as average_age from pets;
```

### 3. Oldest and youngest pets (max and min age)
```sql
select max(age) as oldest_pet, min(age) as youngest_pet from pets;
```

### 4. Total combined age of all pets
```sql
select sum(age) as total_age from pets;
```

---

## Aggregations with GROUP BY (one field)

### 5. Number of pets by species
```sql
select species, count(*) as num_pets
from pets
group by species;
````

### 6. Average age of pets by species

```sql
select species, avg(age) as avg_age
from pets
group by species;
```

### 7. Number of pets by city

```sql
select city, count(*) as num_pets
from pets
group by city;
```

### 8. Average age of pets by city

```sql
select city, avg(age) as avg_age
from pets
group by city;
```

### 9. Oldest pet age by species

```sql
select species, max(age) as oldest_age
from pets
group by species;
```

### 10. Number of pets grouped by birth year
```sql
select year(birthday) as "year", count(*) as "pets per year"
from pets
group by year(birthday);
```

--- 

## Aggregations with GROUP BY (two fields)

### 11. Number of pets by species and city
```sql
select species, city, count(*) as num_pets
from pets
group by species, city;
````

### 12. Average age of pets by species and city

```sql
select species, city, avg(age) as avg_age
from pets
group by species, city;
```

### 13. Number of pets by species and birth year

```sql
select species, year(birthday) as "year", count(*) as num_pets
from pets
group by species, year(birthday);
```

---

## Aggregations with GROUP BY and HAVING

### 14. Show species with more than 3 pets
```sql
select species, count(*) as num_pets
from pets
group by species
having count(*) > 3;
````

### 15. Show cities where the average pet age is greater than 5

```sql
select city, avg(age) as avg_age
from pets
group by city
having avg(age) > 5;
```

### 16. Show birth years with at least 2 pets

```sql
select year(birthday) as "year", count(*) as num_pets
from pets
group by year(birthday)
having count(*) >= 2;
```

---

## Aggregations with GROUP BY, HAVING, and ORDER BY

### 17. List species with their number of pets, ordered from most to least
```sql
select species, count(*) as num_pets
from pets
group by species
order by num_pets desc;
````

### 18. List cities with their average pet age, ordered alphabetically by city

```sql
select city, avg(age) as avg_age
from pets
group by city
order by city asc;
```


-- end --
