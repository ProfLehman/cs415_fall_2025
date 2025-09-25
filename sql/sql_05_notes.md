# SQL-05 notes (Draft)
fall 2025
prof. lehman

## overview

MariaDB is a multi-user database management system. Each user has access rights to one or more databases in the system. The rights to each database vary. For example, as user may be limited to selecting data from one database.  In another database, they may be able to delete data.

## creating a database

`create database` is used to create a database.  A database serves as a collection of related tables. 

```sql
create database database_name;
```

## deleting a database

`drop database` can be used to delete and remove a database.

```sql
drop database database_name;
```

Note: Each student in CS415 may delete (and create) a database with their last name as the identifier. The database is already created.

## Creating a table with a primary key

Create Table is used to create tables.  
Each field is listed with the data type. 
Fields may be Null or Not Null.  
One or more fields are generally listed as the `Primary Key`.
Auto_Increment can be used to assign primary keys sequential numbers when inserting data.

Note: Use the database with your last name to create tables.

```sql
CREATE TABLE person (
	id int NOT NULL AUTO_INCREMENT,
	name varChar(30) NULL,
	major char(4) NULL,
	birthday date NULL,
	PRIMARY KEY (id)
) ENGINE=InnoDB;
```

## Deleting a table

Tables can be deleted with the 'drop table` command.
Notice that the table and data are lost immediately.  **Be Careful!!!**

```sql
drop table person;
```

## Inserting data with field names

```sql
-- fields in the same order as the table
insert into person (id, name, major, birthday) 
values (1,"Alice", "cs", "2005-01-09");

-- field in a different order than the table
insert into person (id, name, major, birthday)
values (2, "cs", "Bob", "2006-12-03");

--this order also works
insert into person (birthday, id, major, name)
       values ("2007-03-03", 3, "cs", "Carol");

-- let auto increment choose id .. 1, 2, 3, 4...
-- thus should be id of 4 if you execute this example in order
insert into person (name, major, birthday)
values ("Dan", "cs", "2002-02-04");

-- this also works as the only field that is required is the id
-- which is an autonumber, thus it creates a new row with
--  5, null, null, null
-- where 5 is the next available id
insert into person () values();

select * from person;
```

## insert statement without field names

Data can be inserted without field names as long as the field order \
matches the table ***and*** all fields are entered.

```sql
insert into person 
values (6,"Fran", "bio", "2009-12-21");

insert into person 
values (7,"MA", "Greta", "2007-12-19");

select * from person;
```

## insert statement with multiple rows

A single insert statement can be used to add multiple rows. 
Notice in this example that the `id` field is not used as `auto_increment` will automatically add the next id.

```sql
insert into person (name, major, birthday)
values ("Hank", "cs", "2003-05-18")
,("Ilsa", "math", "1999-06-09")
,("Jen", "math", "1971-05-18");

select * from person;
```






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


