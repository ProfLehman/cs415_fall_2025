```sql
--
-- SQL-06 Topics (Day 1)
-- your name
-- cs415 fall 2025
--

--create tables member and post
CREATE TABLE person (
	pid integer auto_increment PRIMARY KEY,
	last varChar(10) default "Norman"
)ENGINE=InnoDB;

desc person;

show create table person;

insert into person values();

select * from person;
+-----+--------+
| pid | last   |
+-----+--------+
|   1 | Norman |
+-----+--------+

insert into person (pid) values (1);
ERROR 1062 (23000): Duplicate entry '1' for key 'PRIMARY'

insert into person (pid) values (2);
insert into person (last) values ("jones");

insert into person (last, pid)
values ("mcallister", 43);

insert into person (last)
values ("zedek"), ("eiten"),("alsdkjfl");


alter table person add first varchar(10) default "forester";

alter table person add first varchar(10);

alter table person add first varchar(10)
not null;

alter table person modify first varchar(15)
null default "tbd";

alter table person modify first varchar(5);


update person set first="forester" where pid=1;

alter table person drop column first;

alter table person add age tinyint;
alter table person drop column age;


alter table person add email varchar(50);

-- add a unique constraint to ensure that all email
-- addresses are unique ie. different
alter table person 
add constraint un_email UNIQUE (email);

insert into person (email) values ("norman@huntington.edu");

insert into person (email) values ("norman@aol.com");

 
 
CREATE TABLE sale (
	sid integer auto_increment PRIMARY KEY,
	amount decimal(5,2) default 0,
	pid integer NULL
)ENGINE=InnoDB;


-- adding foreign key will restrict updates
-- and deletes
-- 1. cannot update/delete person if matching records are in sale
-- 2. cannot insert a sale unless it has a matching person
alter table sale 
add constraint fk_pid foreign key (pid)
references person (pid);

-- adding foreign key with cascade means updates
-- and deletes made to person will change sales records.
-- still cannot insert a sale unless it has a matching person
alter table sale 
add constraint fk_pid foreign key (pid)
references person (pid)
ON DELETE CASCADE ON UPDATE CASCADE;

-- remove foreign key
alter table sale drop foreign key fk_pid;


-- store query or "virtual table" by
-- creating a view
create view all_data as
select p.last, s.amount from person p join sale s on p.pid = s.pid;

select * from all_data;


-- drop tables order makes a difference
-- delete many-side first so that there is
-- not matching data
drop table sale;
drop table person;

```
