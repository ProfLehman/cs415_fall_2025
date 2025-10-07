```sql
--
-- cs415 Database Management
-- Assessment 2 review                                      
--

-- 1
CREATE TABLE walker (
	walkerID smallint unsigned,
	name varchar(30),
	phone char(10)
)ENGINE=INNODB;

-- create table with primary key option #1
CREATE TABLE walker2 (
	walkerID smallint,
	name varchar(30),
	phone char(10),
	PRIMARY KEY( walkerID )
)ENGINE=INNODB;

-- create table with primary key option #2
-- also adds constraint for email being unique
CREATE TABLE walker2 (
	walkerID smallint primary key,
	name varchar(30),
	phone char(10)
	email varChar(100) UNIQUE
)ENGINE=INNODB;

insert into walker2 values (-9, "test", "123");


--#2
alter table walker add constraint walker_pk primary key (walkerID);

--#1 & 2
drop table walker;

CREATE TABLE walker (
	walkerID smallint unsigned primary key,
	name varchar(30),
	phone char(10)
)ENGINE=INNODB;

drop table walker;

CREATE TABLE walker (
	walkerID smallint unsigned,
	name varchar(30),
	phone char(10),
	primary key (walkerID)
)ENGINE=INNODB;

-- #3 add a column
alter table walker 
add year int;

--#4 modify column

-- changed field type
alter table walker 
modify year tinyInt;

-- rename column
alter table walker 
change year years tinyInt;

-- #5
alter table walker
alter years set default 1;

-- #6
alter table walker
drop years;

--#7 (see #16)

--#8

--first add data
insert into walker (walkerID, name, phone)
values (2, "Jane Adams", "2193591212"),
(3, "Brad Gordon", "2193591212"),
(7, "Emma Thompson", "2193591212");

--fix phone number for Gordon
update walker set phone = "2193591111" 
where walkerID = 3;

-- set all 219 area codes to 260
update walker set phone = concat("260", right(phone,7) )
where phone like "219%";
--alt
where left(phone,3) = "219";

-- #9
Create Table sponsor (
 id smallInt auto_increment NOT NULL Primary Key,
 name varChar(20),
 amount decimal(6,2) NOT NULL default 20.0,
 date date NOT NULL,
 walkerID smallInt unsigned NOT NULL ,
 CONSTRAINT fk_walkerID FOREIGN KEY (walkerID) REFERENCES walker(walkerID)
)ENGINE=INNODB;

-- drop foreign key constraint
alter table sponsor drop foreign key fk_walkerID;

-- add foreign key constraint
alter table sponsor 
add constraint fk_walkerID foreign key (walkerID)
references walker (walkerID)
ON DELETE CASCADE ON UPDATE CASCADE;


--#10
insert into sponsor (name, date, walkerId) 
values ('Bob Smith', '2005-10-2', 2);

--#11
insert into sponsor (walkerId, date, amount, name) 
values (2, '2005-10-2', 100.00, 'Betty Anderson');

--#12
insert into sponsor (name, date, amount, walkerId) 
values ('Jose Rodriguez', '2005-10-3', 50.0, 3),
('Joel Rogers', '2005-9-3', 22.50,  3);

--check limits of auto increment
insert into sponsor (id, walkerId, date, amount, name) 
values (32768, 2, '2005-10-2', 100.00, 'the Joker');

insert into sponsor (id, walkerId, date, amount, name) 
values (32767, 2, '2005-10-2', 100.00, 'the Joker');

-- add another record
insert into sponsor (name, date, walkerId) 
values ('Paul Whitman', '2005-10-9', 7);

--#13
update sponsor set walkerId = 2 where walkerId = 3;

insert into walker (walkerID, name, phone)
values (3, "Brad Gordon", "2193591212");

--#14
delete from walker where name = 'Brad Gordon';

--#15
insert into sponsor (name, date, amount, walkerId)
select name, curDate(), 25.00, walkerID from walker 
where walkerId = 2;

--#16
-- unique constraint should be used for alternate primary keys
-- any time a field should be unique and it is not the primary key
--
--  hu id (Primary)
--  email 
--  SSN
--  cell phone ??? maybe


-- add field for index
alter table walker add email varchar(100);

-- create index
create unique index ix_walker_email on walker(email);

--drop unique index
drop index ix_walker_email on walker;

--#17
-- char - fixed amount of space
-- varChar(X) - variable amount of storage up to x, 1 length + 1 char up to 255 (2 for length 256+)

--#18
-- script file is a text file with sql commands
-- can use comments -- within file
-- run script with source commands
-- following runs the file file.sql
source file.sql;

--#19
-- with cascade, changes in one table are made to table with foreign key
-- can specify changes when deleting or updating
-- ie. for tables walker has many sponsors with "on delete cascade"
--        if you delete walker, the corresponding sponsors are deleted
--

--#20
begin;
delete from sponsor;
delete from walker;
rollback;

--#21
begin;
delete f
rom sponsor where id=1;
select * from sponsor;
commit;

--#22 Concurrency problems
-- lock ensures that only one statement/transaction can change a table at a time
-- prevents the same airline seat or ticket being sold
-- prevents add two students to the last open seat in a course
-- a "lock" limits who can access a table, ie. when process A has a "lock" on table1, 
--   then it is the only process that can make changes

--#23 ACID 
--
-- Atomicity - A transaction is a logical unit of work that should be completely done or else not done at all
-- Consistency - When complete, data is in a valid state
-- Isolation - No other users see any parts of the transaction until it is completed
-- Durability - When finished, all parts of transaction persist

--#24
-- InnoDB needed for foreign keys, unique indexes, and primary keys, transactions

--#25
-- tinyInt is 1 byte (-128 to 127 or 0 to 255)
-- int is 4 bytes 
-- save 3 bytes

-- creating a view
-- simplifies queries
create view alldata2 AS
select walker.name as "walker", sponsor.name as "sponsor"
from walker join sponsor 
on walker.walkerid = sponsor.walkerid;

-- can now see walker and sponsor using view
select * from alldata;

-- and apply queries
select * from alldata where walker = "Jane Adams";

--- end ---
```













