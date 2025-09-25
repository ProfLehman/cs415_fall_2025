# SQL-05 Notes

fall 2025
prof. lehman

SQL-05 topics
- Data Manipulation: INSERT, UPDATE, DELETE 
- transactions (BEGIN, COMMIT, ROLLBACK)
- ACID


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
Fields may be `Null` or `Not Null`.  
One or more fields are generally listed as the `Primary Key`.
`Auto_Increment` can be used to assign primary keys sequential numbers when inserting data.

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

## Insert rows with field names

```sql
-- fields in the same order as the table
insert into person (id, name, major, birthday) 
values (1,"Alice", "cs", "2005-01-09");

-- field in a different order than the table
insert into person (id, name, major, birthday)
values (2, "Bob", "cs", "2006-12-03");

--this order also works
insert into person (birthday, id, major, name)
       values ("2007-03-03", 3, "ma", "Carol");

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

## Insert rows without field names

Data can be inserted without field names as long as the field order
matches the table ***and*** all fields are entered.

```sql
insert into person 
values (6, "Fran", "ma", "2009-12-21");

insert into person 
values (7, "MA", "Greta", "2007-12-19");

select * from person;

```

## Insert multiple rows

A single insert statement can be used to add multiple rows. 
Notice in this example that the `id` field is not used as `auto_increment` will automatically add the next id.

```sql
insert into person (name, major, birthday)
values ("Hank", "cs", "2003-05-18")
,("Ilsa", "ma", "1999-06-09")
,("Jen", "ma", "1971-05-18");

select * from person;

```

## Update single field value

The `update` statement can be used to change field values.
**Warning** Be sure to add the where condition; otherwise, you will update **all** rows.

```sql
update person set name="Francine" where id=6;

select * from person;

```

## Update two field values
```sql
update person set name="franchesca", major="art" where id=6;

select * from person;

```

## Update three field values
```sql
update person set name="fran", major="bio", birthday="2000-01-01" where id=6;

select * from person;

```

## Delete row(s)
One or more rows may be deleted using the `Delete` command.
**Warning** Be sure to add the where condition; otherwise, you will delete **all** rows.

```sql
delete from person where id = 7;

select * from person;

```

## Insert records from another table

```sql
-- create majors table
CREATE TABLE majors (
	major char(4) NOT NULL,
	PRIMARY KEY (major)
) ENGINE=InnoDB;

-- insert records from another table
insert into majors (major) 
select distinct major from person where major is not null;

select * from majors;

```

---

**CRUD** stands for **Create, Read, Update, and Delete**, the four basic operations performed on data in a relational database. *Create* inserts new records, *Read* retrieves existing data, *Update* modifies existing records, and *Delete* removes records. These operations form the foundation of nearly all database applications and are supported through SQL statements such as `INSERT`, `SELECT`, `UPDATE`, and `DELETE`.

**ACID** represents the four key properties of a reliable transaction: **Atomicity** (all operations succeed or none do), **Consistency** (transactions move the database from one valid state to another), **Isolation** (transactions run independently without interfering), and **Durability** (committed changes persist even after failures). Together, ACID ensures that data remains accurate and dependable, even in the presence of errors or concurrent users.

**Transactions** are sequences of one or more SQL operations executed as a single logical unit of work. A transaction begins with `BEGIN` and must be explicitly ended with either `COMMIT`, which saves the changes permanently, or `ROLLBACK`, which undoes them. By grouping CRUD operations inside transactions, databases protect against partial updates and allow developers to recover gracefully from mistakes or unexpected errors.

---
## Transactions that roll back

`begin` and 'rollback' will **undo** most changes to the database.

```sql
begin;
delete from person;
select * from person;
rollback;
```

## Transactions that commit

`begin` and 'commit' will **keep** most changes to the database.

```sql
begin;
update person set major = "cs";
select * from person;
commit;
```

Note: In MariaDB, transactions require the InnoDB storage engine because it is designed to support ACID properties. Unlike MyISAM (which lacks transaction control), InnoDB provides features such as row-level locking, rollback, and crash recovery, making it the standard choice for reliable transaction processing.

--- end ---


