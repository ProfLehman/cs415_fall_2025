# Book Author Joins Example


## ER Model

```mermaid
erDiagram
    AUTHOR {
        int aid PK
        varchar name
    }

    BOOK {
        int bid PK
        varchar title
    }

    AUTHORSHIP {
        int aid FK
        int bid FK
    }

    AUTHOR o|--o{ AUTHORSHIP  : writes
    BOOK   o|--o{ AUTHORSHIP  : written_by
```


---

## Creating Tables

Execute the following SQL code in your database to create the book, authorship, author tables

```sql
-- sample database for demonstrating joins (create tables in your database)
--
--
--   author 1:1 <---> 0:M authorship 0:M <---> 1:1 book
--
--   author will have 0 or more authorships
--   book will have 0 or many authorships
--
--   authorship will specify 0 or 1 author and 0 or 1 book
-- 

CREATE TABLE author (
    aid int not null,
	name varchar(32),
	PRIMARY KEY (aid)
) ENGINE=InnoDB;

INSERT INTO author VALUES 
(1, "Alice"),
(2, "Bob"),
(3, "Carol"),
(4, "Dan"),
(5, "Erin");

CREATE TABLE book (
    bid int not null,
	title varchar(32),
	PRIMARY KEY (bid)
) ENGINE=InnoDB;

INSERT INTO book VALUES 
(1, "Awful Ants Are Around"),
(2, "Beautiful Barns"),
(3, "Crazy Coders Create Chaos"),
(4, "Delicious Donuts"),
(5, "Easy Excellent Eggs");

CREATE TABLE authorship (
    aid int,
	bid int
) ENGINE=InnoDB;

INSERT INTO authorship VALUES 
(1, 4),
(3, 1),
(6, 5),
(5, 1),
(4, 5),
(4, 2),
(5, 6);

```
---
# View rows in each table

Run the following SQL to see the rows in each table

```sql

select * from author;
+-----+-------+
| aid | name  |
+-----+-------+
|   1 | Alice |
|   2 | Bob   |
|   3 | Carol |
|   4 | Dan   |
|   5 | Erin  |
+-----+-------+

select * from book
+-----+---------------------------+
| bid | title                     |
+-----+---------------------------+
|   1 | Awful Ants Are Around     |
|   2 | Beautiful Barns           |
|   3 | Crazy Coders Create Chaos |
|   4 | Delilicious Donuts        |
|   5 | Easy Excellent Eggs       |
+-----+---------------------------+

select * from authorship;
+------+------+
| aid  | bid  |
+------+------+
|    1 |    4 |
|    3 |    1 |
|    6 |    5 |
|    5 |    1 |
|    4 |    5 |
|    4 |    2 |
|    5 |    6 |
+------+------+
```
---

## Practice Questions


### Cross Product Basics

   How many rows result when you take the cross product of the `author` and `authorship` tables?
   
   x2 table cross product author and authorship
   x5 rows * x8 rows = 35 rows (every combination) 

   How many rows result when you take the cross product of the `author`, and `authorship` '`and book` tables?
   
   x3 table cross product author and authorship and book
   x5 rows * x8 rows * x5 = 175 rows (every combination) 


```sql
select count(*) from author, authorship;
+----------+
| count(*) |
+----------+
|       35 |
+----------+

select count(*) from author, authorship, book;
+----------+
| count(*) |
+----------+
|      175 |
+----------+

```


### x2 table join via cross product of author and authorship

```sql

select author.aid, authorship.aid, author.name, authorship.bid
from author, authorship
where author.aid = authorship.aid;

+-----+------+-------+------+
| aid | aid  | name  | bid  |
+-----+------+-------+------+
|   1 |    1 | Alice |    4 |
|   3 |    3 | Carol |    1 |
|   5 |    5 | Erin  |    1 |
|   4 |    4 | Dan   |    5 |
|   4 |    4 | Dan   |    2 |
|   5 |    5 | Erin  |    6 |
+-----+------+-------+------+

-- Generally would only show one copy of the aid (can use either table)
select author.aid, author.name, authorship.bid
from author, authorship
where author.aid = authorship.aid;

-- using alias
select a.aid, a.name, au.bid
from author a, authorship au
where a.aid = au.aid;

+-----+-------+------+
| aid | name  | bid  |
+-----+-------+------+
|   1 | Alice |    4 |
|   3 | Carol |    1 |
|   5 | Erin  |    1 |
|   4 | Dan   |    5 |
|   4 | Dan   |    2 |
|   5 | Erin  |    6 |
+-----+-------+------+
```


### x2 table join via JOIN ON of author and authorship

```sql

select author.aid, author.name, authorship.bid
from author JOIN authorship
ON author.aid = authorship.aid;

-- using alias
select a.aid, a.name, au.bid
from author a JOIN authorship au
ON a.aid = au.aid;

+-----+-------+------+
| aid | name  | bid  |
+-----+-------+------+
|   1 | Alice |    4 |
|   3 | Carol |    1 |
|   5 | Erin  |    1 |
|   4 | Dan   |    5 |
|   4 | Dan   |    2 |
|   5 | Erin  |    6 |
+-----+-------+------+
```


### left join of author and authorship
ALL data in author (left) that matches with right, if author does not have match, show null

```sql
select a.aid, a.name, au.bid
from author a LEFT JOIN authorship au
ON a.aid = au.aid;

+-----+-------+------+
| aid | name  | bid  |
+-----+-------+------+
|   1 | Alice |    4 |
|   3 | Carol |    1 |
|   5 | Erin  |    1 |
|   4 | Dan   |    5 |
|   4 | Dan   |    2 |
|   5 | Erin  |    6 |
|   2 | Bob   | NULL |
+-----+-------+------+
```

### right join of author and authorship

ALL data in authorship (right) that matches with left
if authorship does not have match, show null

```sql
select a.aid, a.name, au.bid
from author a RIGHT JOIN authorship au
ON a.aid = au.aid;

+------+-------+------+
| aid  | name  | bid  |
+------+-------+------+
|    1 | Alice |    4 |
|    3 | Carol |    1 |
| NULL | NULL  |    5 |
|    5 | Erin  |    1 |
|    4 | Dan   |    5 |
|    4 | Dan   |    2 |
|    5 | Erin  |    6 |
+------+-------+------+

-- note: above is same as authorship LEFT JOIN author
--        ie.   tableA left join tableB   same as
--              tableB right join tableA
--

select a.aid, a.name, au.bid
from authorship au LEFT JOIN author a
ON a.aid = au.aid;
```

### full join or full outer join

union of a left and right join
no full join operator in mariadb (duck tape approach)

```sql

select a.aid, a.name, au.bid
from author a LEFT JOIN authorship au
ON a.aid = au.aid

UNION

select a.aid, a.name, au.bid
from author a RIGHT JOIN authorship au
ON a.aid = au.aid;

+------+-------+------+
| aid  | name  | bid  |
+------+-------+------+
|    1 | Alice |    4 |
|    3 | Carol |    1 |
|    5 | Erin  |    1 |
|    4 | Dan   |    5 |
|    4 | Dan   |    2 |
|    5 | Erin  |    6 |
|    2 | Bob   | NULL |
| NULL | NULL  |    5 |
+------+-------+------+

```


### x3 table joins

```sql

--- x3 table cross product inner join
select a.aid, a.name, au.bid, b.title
from author a, authorship au, book b
where a.aid = au.aid
and au.bid = b.bid;

--- x3 inner join using JOIN
select a.aid, a.name, au.bid, b.title
from (author a JOIN authorship au ON a.aid = au.aid)
JOIN book b ON au.bid = b.bid;

+-----+-------+------+-----------------------+
| aid | name  | bid  | title                 |
+-----+-------+------+-----------------------+
|   1 | Alice |    4 | Delilicious Donuts    |
|   3 | Carol |    1 | Awful Ants Are Around |
|   5 | Erin  |    1 | Awful Ants Are Around |
|   4 | Dan   |    5 | Easy Excellent Eggs   |
|   4 | Dan   |    2 | Beautiful Barns       |
+-----+-------+------+-----------------------+
```


### What about Bob? no authorship record

```sql
select a.aid, a.name, au.bid, b.title
from (author a LEFT JOIN authorship au ON a.aid = au.aid)
LEFT JOIN book b ON au.bid = b.bid;

+-----+-------+------+-----------------------+
| aid | name  | bid  | title                 |
+-----+-------+------+-----------------------+
|   1 | Alice |    4 | Delilicious Donuts    |
|   3 | Carol |    1 | Awful Ants Are Around |
|   5 | Erin  |    1 | Awful Ants Are Around |
|   4 | Dan   |    5 | Easy Excellent Eggs   |
|   4 | Dan   |    2 | Beautiful Barns       |
|   5 | Erin  |    6 | NULL                  |
|   2 | Bob   | NULL | NULL                  |
+-----+-------+------+-----------------------+
```

### Dan's books

```sql
select a.aid, a.name, au.bid, b.title
from (author a JOIN authorship au ON a.aid = au.aid)
JOIN book b ON au.bid = b.bid
WHERE a.name = "Dan" ORDER by b.title;

+-----+------+------+---------------------+
| aid | name | bid  | title               |
+-----+------+------+---------------------+
|   4 | Dan  |    2 | Beautiful Barns     |
|   4 | Dan  |    5 | Easy Excellent Eggs |
+-----+------+------+---------------------+
```

### authors and number of book authorships
aggregation, group by

```sql
select aid, count(bid) from authorship group by aid;

+------+------------+
| aid  | count(bid) |
+------+------------+
|    1 |          1 |
|    3 |          1 |
|    4 |          2 |
|    5 |          2 |
|    6 |          1 |
+------+------------+

```

### authors and number of book authorships
aggregation, group by, having

```sql

select aid, count(bid) 
from authorship 
group by aid
having count(bid) > 1;

+------+------------+
| aid  | count(bid) |
+------+------------+
|    4 |          2 |
|    5 |          2 |
+------+------------+
```


### inner join via cross product with aggregation

```sql
select author.aid, author.name, count(authorship.bid) 
from author, authorship
where author.aid = authorship.aid 
group by authorship.aid
having count(authorship.bid) > 1;

+-----+------+-----------------------+
| aid | name | count(authorship.bid) |
+-----+------+-----------------------+
|   4 | Dan  |                     2 |
|   5 | Erin |                     2 |
+-----+------+-----------------------+
```

--- end ---


