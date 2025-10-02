```sql
--
-- SQL-06 Topics (Day 2)
-- lehman
-- cs415 fall 2025
--

insert into person (last, bday)
values ("Forester", "1897-08-01");

CREATE TABLE person (
	pid integer auto_increment PRIMARY KEY,
	last varChar(20) default,
	bday date
)ENGINE=InnoDB;

-- integer 4 bytes
-- varChar(20) 1 byte length plus 1 byte each CHARACTER
--  so "Foreseter" is 9 bytes plus 1 for length = 10 bytes
-- date is 3 bytes
-- total bytes: 17


-CREATE TABLE person (
	pid smallint auto_increment PRIMARY KEY,
	last char(20) default,
	bday date
)ENGINE=InnoDB;

-- small integer 2 bytes
-- char(20) 20 bytes no matter what is stored
--  so "Foreseter" is 20
-- date is 3 bytes
-- total bytes: 25





-- referential integrity

CREATE TABLE person (
	pid integer auto_increment PRIMARY KEY,
	last varChar(10) default "Norman"
)ENGINE=InnoDB;

insert into person (last) values
("Alice"),("Bob"),("Carol");


CREATE TABLE sale (
	sid integer auto_increment PRIMARY KEY,
	amount decimal(5,2) default 0,
	pid integer NULL,
	constraint fk_pid foreign key (pid) references person (pid)
	ON DELETE RESTRICT
	ON UPDATE CASCADE
)ENGINE=InnoDB;

-- work as there is a matching pid in person
insert into sale (amount, pid) VALUES (200.00, 1);
insert into sale (amount, pid) VALUES (400.00, 1);
insert into sale (amount, pid) VALUES (500.00, 3);

-- error with foreign key
insert into sale (amount, pid) VALUES (600.00, 4);

-- change to pid in person will "cascade" sale
update person set pid = 5 where pid = 1;

-- can not delete from person if matching row in sale
delete from person where pid=5;

-- ok to delete person if no matching row in sale
delee from person where pid=2

-- delete sale, then delete person
drop table sale;
drop table person;



-- re-create database

CREATE TABLE person (
	pid integer auto_increment PRIMARY KEY,
	last varChar(10) default "Norman"
)ENGINE=InnoDB;

insert into person (last) values
("Alice"),("Bob"),("Carol");

CREATE TABLE sale (
	sid integer auto_increment PRIMARY KEY,
	amount decimal(5,2) default 0,
	pid integer NULL,
	constraint fk_pid foreign key (pid) references person (pid)
	ON DELETE CASCADE
	ON UPDATE CASCADE
)ENGINE=InnoDB;

insert into sale (amount, pid) VALUES (200.00, 1);
insert into sale (amount, pid) VALUES (400.00, 1);

insert into sale (amount, pid) VALUES (200.00, 4);
insert into sale (amount, pid) VALUES (400.00, 4);


insert into sale (amount, pid) VALUES (500.00, 3);

-- deleting person deletes their sales as the delete is "cascaded"
delete from person where pid = 1;


select person.pid, person.last, sale.amount
from person join sale on person.pid = sale.pid;


select person.pid, person.last, sale.amount
from person join sale on person.pid = sale.pid
where sale.amount >= 400;

-- VIEW
create view data as
select person.pid, person.last, sale.amount
from person join sale on person.pid = sale.pid;

select * from data;

select * from data where amount >= 400;

desc data;
+--------+--------------+------+-----+---------+-------+
| Field  | Type         | Null | Key | Default | Extra |
+--------+--------------+------+-----+---------+-------+
| pid    | int(11)      | NO   |     | 0       |       |
| last   | varchar(10)  | YES  |     | Norman  |       |
| amount | decimal(5,2) | YES  |     | 0.00    |       |
+--------+--------------+------+-----+---------+-------+

-- create view
create view nosales as
select person.pid, person.last
from person left join sale on person.pid = sale.pid
where sale.amount IS null;

-- can query view
select * from nosales;

-- will show view as a table
show create table data;


-- drop view
drop view nosales;


-- another example ...

CREATE TABLE patron (
	id integer auto_increment PRIMARY KEY,
	last varChar(30) NOT NULL default "TBA"
)ENGINE=InnoDB;

desc patron;

insert into patron (last) values ("Smith");

insert into patron values();

update patron set last = "Whatever You Want" where id=2;

insert into patron (id, last) values (3,"Nalliah");
 
alter table patron add birthday date null;

desc patron;
 
desc person;

CREATE TABLE ticket (
	id integer auto_increment PRIMARY KEY,
	event varChar(30) NOT NULL default "fun",
	date date null
)ENGINE=InnoDB;

desc ticket;

alter table ticket add pid integer not null;
desc ticket;


-- adding foreign key will restrict updates
-- and deletes
-- 1. cannot update/delete person if matching records are in ticket
-- 2. cannot insert a ticket unless it has a matching patron
alter table ticket 
add constraint fk_pid foreign key (pid)
references patron (id);

alter table ticket drop foreign key fk_pid;

-- adding foreign key with cascade means updates
-- and deletes made to patron will change ticket records.
-- still cannot insert a ticket unless it has a matching patron
alter table ticket 
add constraint fk_pid foreign key (pid)
references patron (id)
ON DELETE CASCADE ON UPDATE CASCADE;

-- ? how to delete tables?
drop table ticket;
drop table patron;

-- end ---
```






