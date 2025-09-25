
```sql

-- SQL-05 notes (Draft)
-- fall 2025
-- prof. lehman

-- show databases;

-- use the database with your last name to create tables

-- create database_name;
-- drop database database_name;

-- see SQL create
-- show create table_name 

-- drop table table_name



-- 7-1 Create a table with five or more fields.  Include a primary key.  
--- Include int, varchar, char, and date field types.

CREATE TABLE person (
	id int NOT NULL AUTO_INCREMENT,
	name varChar(30) NULL,
	major char(4) NULL,
	birthday date NULL,
	PRIMARY KEY (id)
) ENGINE=InnoDB;



-- 7-2 Create an insert statement to add a new record using field names similar to example shown.

insert into person (id, name, major, birthday)
values (1,"alice", "cs", "1992-01-09");

-- need to keep field order correct
insert into person (id, name, major, birthday)
values (1,"cs", "Alic", "1992-01-09");

--this order also works
insert into person (id, major, name,   birthday)
       values      (1,  "cs", "Alice", "1992-01-09");

-- let auto increment choose id .. 1, 2, 3, 4...
insert into person (name, major, birthday)
values ("alice", "cs", "1992-01-09");

-- this also works as the only field that is required is the id
-- which is an autonumber thus it creates a row
--  5, null, null, null
-- where 5 is the next available id
insert into person () values();



-- 7-3 Create an insert statement that inserts two or more rows

insert into person (id, name, major, birthday)
values (2,"bob", "cs", "1992-05-18")
,(3,"carol", "math", "1994-06-09") ;



-- 7-4  Create an insert statement without field names
--      The field order must match the order for table create

insert into person 
values (6,"greta", "bio", "1993-12-11");

insert into person 
values (7,"MA", "Erik", "1993-12-11");



-- 7-5 Create a second table and use an insert statement to fill the table using data from your table from # 7-1.

CREATE TABLE majors (
	major char(4) NOT NULL,
	PRIMARY KEY (major)
) ENGINE=InnoDB;

-- insert records from another table
insert into majors (major) 
select distinct major from person where major is not null;

select * from majors;


-- 7-6 Create a delete statement that deletes one or more rows based on a where condition.
	
	delete from person where id = 7;


-- 7-7 Create an update statement that sets one values.

	update person set name="franklin" where id=6;


-- 7-6 Create an update statement that sets two values.

	update person set name="frank", major="cs" where id=6;


-- 7-9 Create a transaction that either deletes or inserts records, then rolls back the changes.

begin;
delete from person;
select * from person;
rollback;


-- 7-10 Create a transaction that either updates or inserts records, then commits the changes.

begin;
update person set major = "cs";
select * from person;
commit;

```
--- end ---


