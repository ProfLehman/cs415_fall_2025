```sql
-- ch9 security
-- fall 2021 (updated from fall 2019, 2017, fall 2015) 
-- j.l. lehman

-- Security
-- mariaDB usernames and passwords are independent of the OS usernames and passwords
-- all mariaDB usernames must have a password (other wise any user can log in using this username)
-- usernames are limited to 80 characters in length

-- +--------------------------------+
-- | Passwords                      |
-- +--------------------------------+

-- change your own password
SET PASSWORD = PASSWORD('newPassword');

-- password function returns a password string for storage in the user table
-- the string is the result of a one-way hash
-- note: old_password used in MySQL 4.1 or later, how does length differ?
select password("is this a secure password?");
select length( password("is this a secure password?") );

select old_password("is this a secure password?");
select length( old_password("is this a secure password?") );


-- admin - change password
SET PASSWORD FOR 'bob'@'localhost' = PASSWORD('mypassword');


-- +--------------------------------+
-- | Flush Privileges               |
-- +--------------------------------+
-- Flush Privileges ensures changes to mysql database have been updated
flush privileges;


-- +--------------------------------+
-- | create new users using CREATE  |
-- +--------------------------------+

-- using create statement password is blank by default
-- note: for CS415 assignment you need to use grant to create users
CREATE USER 'jones'@'localhost';

use mysql;
select user, host, password from user where user = 'jones';
+------------+-----------+-------------------------------------------+
| user       | host      | password                                  |
+------------+-----------+-------------------------------------------+
| jones      | localhost |                                           |
+------------+-----------+-------------------------------------------+

-- +-----------------+
-- | remove a user   |
-- +-----------------+
drop user jones@localhost;


-- using create statement with password (test is password name)
CREATE USER 'jones'@'localhost' identified by "cs415";

use mysql;
select user, host, password from user where user = 'jones';
+-------+-----------+-------------------------------------------+
| user  | host      | password                                  |
+-------+-----------+-------------------------------------------+
| jones | localhost | *5C1718D92468FAEE0533EEF558169FE30ED4AD83 |
+-------+-----------+-------------------------------------------+



-- using create statement password is blank by default, host is % (any location) by default
FalCREATE USER jones;

use mysql;
select user, host, password from user where user = "jones";
+-------+------+----------+
| user  | host | password |
+-------+------+----------+
| jones | %    |          |
+-------+------+----------+


-- see current user and host
select user();
select current_user();


-- +--------------------------------+
-- | create database                |
-- +--------------------------------+
CREATE DATABASE jones;


-- +---------------------------------------------+
-- | grant access to database (and create users) |
-- +---------------------------------------------+
GRANT ALL ON jones.* to 'jones'@'localhost';
GRANT ALL ON jones.* to 'jones'@'localhost' WITH GRANT OPTION;

-- The "WITH GRANT OPTION" allows user to create users for their own databases
-- however, they must have access to the mysql database

-- note: grant can also be use to create users
--      if jones@localhost was not a user, 
--      a new user would be created

-- Give bob all privileges (except for granting privileges) to database bob
-- this also gives bob a password and makes the default host %
GRANT ALL ON bob.* to 'bob'@'localhost' IDENTIFIED BY 'password';



-- +--------------------------+
-- | Table Level Privileges   |
-- +--------------------------+
-- Give Bob select privilege on the Artists table from bob database
--   can also include update, delete 
-- ie. grant select, update, delete on bob.Artists to 'bob'@'localhost';
grant select on bob.Artists to 'bob'@'localhost';


-- +--------------------------+
-- | Column Level Privileges  |
-- +--------------------------+
--Give Bob select privilege on the columns Title and Genre
grant select (Title, Genre) on bob.Titles to 'bob'@'localhost';



-- +-------------------------------------------------+
-- | create a user with out access to any databases  |
-- +-------------------------------------------------+
grant usage on *.* to 'betty'@'localhost' identified by 'password';


-- +------------------------------------+
-- | creating new root or "superuser"s  |
-- +------------------------------------+
GRANT ALL ON *.* TO 'superuser' IDENTIFIED BY 'password';
GRANT ALL ON *.* TO 'superuser' IDENTIFIED BY 'password' WITH GRANT OPTION


-- +-----------------+
-- + place limits    +
-- +-----------------+
GRANT ALL ON customer.* TO 'franklin'@'localhost'
IDENTIFIED BY 'frank'
WITH MAX_QUERIES_PER_HOUR 2
MAX_UPDATES_PER_HOUR 10
MAX_CONNECTIONS_PER_HOUR 5;


-- +---------------------------------------------+
-- | display grants                              |
-- +---------------------------------------------+

--list privileges for the current session
SHOW GRANTS;
SHOW GRANTS FOR CURRENT_USER;
SHOW GRANTS FOR CURRENT_USER();
SHOW GRANTS 'bob'@'localhost';


--This statement lists the GRANT statements that must be issued
--to duplicate the privileges for a MySQL user account.

SHOW GRANTS FOR 'root'@'localhost';
+---------------------------------------------------------------------+
| Grants for root@localhost                                           |
+---------------------------------------------------------------------+
| GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION |
+---------------------------------------------------------------------+


-- +-------------------------------+
-- | remove privileges with revoke |
-- +-------------------------------+
REVOKE ALL ON bob.* from bob@localhost;

REVOKE select on bob.Artists from bob@localhost;

REVOKE select (Title, Genre) on bob.Titles from bob@localhost;


-- +-------------------------------+
-- | remove user                   |
-- +-------------------------------+
-- note: does not delete the databases this user can access
DROP USER jones@localhost;


-- +-------------------------------+
-- | remove database               |
-- +-------------------------------+
DROP DATABASE jones;


-- +-------------------------------+
-- | create view                   |
-- +-------------------------------+
create view test1 as select TrackTitle, LengthSeconds/60 AS minutes from Tracks;


-- views are defined in the information_schema database
use information_schema

select * from VIEWS\G


-- +-------------------------------+
-- | create view                   |
-- +-------------------------------+
drop view test1;


-- +---------- end of file --------+
```























