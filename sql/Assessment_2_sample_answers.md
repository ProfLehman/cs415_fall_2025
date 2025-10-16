
#  Assessment #2 Sample Solutions
CS415 Database Management
Fall 2025

## SQL-04 Joins

```sql
-- create sample tables and insert data

CREATE TABLE member (
  mid int(11) NOT NULL,
  name varchar(20) DEFAULT NULL,
  state char(2) DEFAULT NULL,
  PRIMARY KEY (mid)
) ENGINE=InnoDB;

INSERT INTO member (mid, name, state)
VALUES 
(10, 'Alice', 'IN'),
(11, 'Bob', 'OH'),
(12, 'Carol', 'MI'),
(13, 'Dan', 'IN'),
(14, 'Erin', 'CA');


CREATE TABLE book (
  bid int(11) NOT NULL,
  title varchar(40) DEFAULT NULL,
  author varchar(20) DEFAULT NULL,
  PRIMARY KEY (`bid`)
) ENGINE=InnoDB;

INSERT INTO book (bid, title, author)
VALUES
(1, 'Database Systems', 'Elmasri'),
(2, 'Artificial Intelligence', 'Russell'),
(3, 'Computer Networks', 'Tanenbaum'),
(4, 'Introduction to Algorithms', 'Alice'),
(5, 'Operating System Concepts', 'Silberschatz');


CREATE TABLE checkout (
  cid int(11) NOT NULL,
  date date DEFAULT NULL,
  bid int(11) DEFAULT NULL,
  mid int(11) DEFAULT NULL,
  PRIMARY KEY (cid)
) ENGINE=InnoDB;

INSERT INTO checkout (cid, date, bid, mid)
VALUES
(201, '2025-10-05', 1, 10),
(202, '2025-10-10', 3, 11),
(203, '2025-10-12', 3, 12),
(204, '2025-10-15', 5, 14);

-- 1.
-- How many rows would be returned by the following cross product?
SELECT count(*) 
FROM book, checkout, member;

-- 5 x 4 x 5 = 100 rows


-- 2. Complete the following to implement a cross product join of tables book and
--    checkout displaying the title and checkout date for all books with checkouts.

SELECT b.title, c.date
FROM book b, checkout c
WHERE b.bid = c.bid;


-- 3.
--  Complete the following using an Inner Join (ie. JOIN keyword) to display the same results as #2.

SELECT b.title, c.date
FROM book b JOIN checkout c
ON b.bid = c.bid;

-- can also specify INNER but "JOIN" and "INNER JOIN" are same
SELECT b.title, c.date
FROM book b INNER JOIN checkout c
ON b.bid = c.bid;


-- 4.
-- Complete the following left join of tables member and checkout.

SELECT m.name, c.date
FROM member m LEFT JOIN checkout c
ON m.mid = c.mid;


-- 5.
-- Show the results of checkout right join book. Display the mid and bid only. (hint: x6 rows)  Show the data returned, not the SQL

| mid  | bid |
|------|-----|
| 10   | 1   |
| 11   | 3   |
| 12   | 3   |
| 14   | 5   |
| NULL | 2   |
| NULL | 4   |


-- 6.
-- What is a full outer join?  In general (not exact SQL), how can a full outer join be accomplished with MariaDB? (2 or 3 sentences)

A full outer join returns all rows from both tables. Matching rows are combined, and non-matching rows show NULL values for the missing side.
MariaDB does not have a built-in FULL OUTER JOIN, but it can be simulated using a UNION of a LEFT JOIN and a RIGHT JOIN, for example:

SELECT * FROM A LEFT JOIN B ON A.id = B.id
UNION
SELECT * FROM A RIGHT JOIN B ON A.id = B.id;


-- 7.
-- Complete the following to join all three tables to display the member name, checkout date, and book as shown.  You may use cross product or join approach.

SELECT m.name, c.date, b.title
FROM member m
JOIN checkout c ON m.mid = c.mid
JOIN book b ON c.bid = b.bid;

-- or with cross product
SELECT m.name, c.date, b.title
FROM member m, checkout c, book b
WHERE m.mid = c.mid
AND c.bid = b.bid;


-- 8.
-- Show all member and author names without duplicates as shown. (one SQL statement)

SELECT name FROM member
UNION
SELECT author AS name FROM book;

```


## SQL-06 Data Definition

```sql
CREATE TABLE artist (
  aid char(3) PRIMARY KEY,
  name varChar(30)
) ENGINE=INNODB;

insert into artist values ("a11", "George Winston"),
("a22", "Harry Connick"),
("a33", "Jars Of Clay"),
("a44", "Rippingtens");
```

```sql

-- 1
CREATE TABLE cd (
  cid int auto_increment NOT NULL Primary Key,
  title varChar(50) NOT NULL default "New Release",
  available date NULL,
  aid char(3) NOT NULL
)ENGINE=INNODB;

-- minimal NOT NULL's - null is default unless primary key
CREATE TABLE cd (
  cid int auto_increment Primary Key,
  title varChar(50) NOT NULL default "New Release",
  available date NULL,
  aid char(3) NOT NULL
)ENGINE=INNODB;

-- specify primary key on separate line
CREATE TABLE cd (
  cid int auto_increment NOT NULL,
  title varChar(50) NOT NULL default "New Release",
  available date NULL,
  aid char(3) NOT NULL,
  primary key (cid)
)ENGINE=INNODB;

-- add data to cd
insert into cd (title, available, aid) values
("Jars Of Clay","2015-10-24", "a33"),
("Blue Light", "2014-08-30", "a22"),
("Kilimanjaro", "2009-12-20", "a44"),
("Topaz", "2008-05-18", "a44"),
("December", NULL, "a11"),
("New Release", "2018-10-08", "a11");  

-- 3
-- Use char for fixed length fields 
-- ie. SSN, state abreviations, zip, phone#
-- 1 byte per character even if spaces char(4) always 4 bytes
--
-- Use varChar for any field with varying length
-- ie. names, cities, titles, etc ... 
-- Save some space as varChar stores length (1 byte) for each field
-- if length is 0 to 255 uses 1 byte for length 
--     plus 1 byte for each character
-- if length is 256+ uses 2 bytes for length 
--     plus 1 byte per character
--
-- Using char can help with search performance 
-- depending on physical implementation as fixed length
-- is easier to determine field location in file

-- 3
-- (1, “Oct”, “2025-10-09”, “IN”) 
-- int, varChar(20), date, and char(2)? 
--
-- 1 => int => 4 bytes
-- "Oct" => varChar(20, 
--    1 byte length plus one for each letter/space 
--    thus 1 + 3 => 4 bytes
-- "2023-10-12" => date => 3 bytes
-- "IN" => char(2) => 2 bytes
-- total = 13 bytes

-- 4
alter table artist add email varChar(60);
alter table artist add column email varChar(60);

-- 5
alter table artist drop email;
alter table artist drop column email;

-- 6
alter table artist modify name varChar(50);
alter table artist modify column name varChar(50);

-- 7
-- c. Eliminates duplicate titles

-- 8
alter table cd add constraint foreign key fk_aid(aid) references artist(aid) 
on delete restrict on update restrict;

alter table cd add constraint fk_aid foreign key (aid) references artist(aid) 
on delete restrict on update restrict;

--note: by default on delete and on update are set to restrict thus optional
alter table cd add constraint foreign key fk_aid(aid) references artist(aid);
alter table cd add constraint fk_aid foreign key (aid) references artist(aid);


-- 9
alter table cd drop foreign key fk_aid;
alter table cd drop  fk_aid;

-- 10 On Delete Cascade
--
-- a. When a cd record is deleted, the matching artist record is also deleted (false)
--
-- When a cd record is deleted, only that record is removed.  
-- The artist table is not affected.
--
-- b. When an artist record is deleted, the matching cd records are also deleted (true)
--
-- When an artist record is deleted, all of the matching CD records are also deleted as 
-- the changes are cascaded.
--

--
alter table cd add constraint fk_aid foreign key (aid) references artist(aid) 
on delete cascade on update cascade;

-- 11
create view rips as
select *
from cd
where artist.aid = "a44";

create view rips
select *
from cd
where artist.aid = "a44";

-- 12
select * from rips;
```

## SQL-05 Data Manipulation

```sql
-- 1  
insert into artist values ("a55", "Pink Martini");
insert into artist (aid, name) values ("a55", "Pink Martini");
--note "value" also  works

-- 2
insert into artist (aid, name) values  ("a66", "Alex Pangman"), ("a77", "Norah Jones");
insert into artist values ("a66", "Alex Pangman"), ("a77", "Norah Jones");
--note "value" also  works

-- 3
insert into artist (name)
select name from new_artist;

-- 4
update cd set available = "2021-08-15" where cid = 5;
update cd set available = "2021-08-15" where title = "December";

-- 5
update artist set name = "Rippingtons" where aid = "a44";


-- 6
delete from cd where cid=4;
delete from cd where title="Topaz";
.

-- 7
begin;
delete from cd where cid = 4;
rollback;

-- 8
begin;
delete from cd where cid = 4;
commit;

begin transaction;
delete from cd where cid = 4;
commit;

-- 9
-- Concurrency problems arise when two or more users must access and change one or more tables.
-- This can lead to corrupted data.
-- Examples can include tickets (movies, concerts, airlines), hotel room bookings, any type of scheduling, with drawel of funds, etc...

-- 10
-- ACID (Atomicity, Consistency, Isolation, Durability) 
--
-- Atomicity - A transaction is a logical unit of work that should be completely done or else not done at all
--
-- Consistency - When complete, data is in a valid state
--
-- Isolation - No other users see any parts of the transaction until it is completed
--
-- Durability - When finished, all parts of transaction persist
--

-- end --
