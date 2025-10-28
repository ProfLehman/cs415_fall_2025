# CS 415 Database Management Systems 
## Lab-01 – Import/Export - 40 Points
## Recommended Due: 04 November 2025 (Final Due:  04 December 2025 at 5 pm.)

---

The purpose of this assignment is learn how import and export data with MariaDB.

We will be using Microsoft Access (Windows Only) for this assignment. You can use Microsoft Access in the Computer Labs (S175/177).

See [office Portal](https://portal.office.com) to download Access on a Windows computer.

Pick a **single table** from your final project to complete Parts 1 to 4.

### Part 1.  Backup Database
Save a copy of your table create and insert statements using mysqldump in a file called lab1.sql

### Part 2.  Comma-Delimited (CSV – comma-separated values)
Save the table as a comma-delimited file called lab1.csv

### Part 3.  CSV to Excel
Import your file from Part 2 into Excel and save the file (in Excel format) as lab1.xlsx

### Part 4.  Microsoft Access

    1. Create an Access database called lab1.accdb

    2. Create and save query to create your table in Access

    3. Copy and paste your data from the Excel Spreadsheet (Part 3) into your table

    4. Create and save two sample queries for your table

    5. Create and save two sample reports for your table



Upload zip file of the following four files.
    1. lab1.sql
    2. lab1.csv
    3. lab1.xlsx
    4. lab1.accdb

---

### Sample Artist table

```
SQL

CREATE TABLE `Artists` (
  `ArtistID` int(11) NOT NULL,
  `ArtistName` varchar(50) NOT NULL,
  `City` varchar(25) DEFAULT NULL,
  `Region` varchar(15) DEFAULT NULL,
  `Country` varchar(20) DEFAULT NULL,
  `WebAddress` varchar(40) DEFAULT NULL,
  `EntryDate` date DEFAULT NULL,
  `LeadSource` varchar(10) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

INSERT INTO `Artists` VALUES (1,'The Neurotics','Peterson','NC','USA','www.theneurotics.com','2003-05-14','Directmail'),(2,'Louis Holiday','Clinton','IL','USA',NULL,'2003-06-03','Directmail'),(3,'Word','Anderson','IN','USA',NULL,'2003-06-08','Email'),(5,'Sonata','Alexandria','VA','USA','www.classical.com/sonata','2003-06-08','Ad'),(10,'The Bullets','Alverez','TX','USA',NULL,'2003-08-10','Email'),(14,'Jose MacArthur','Santa Rosa','CA','USA','www.josemacarthur.com','2003-08-17','Ad'),(15,'Confused','Tybee Island','GA','USA',NULL,'2003-09-14','Directmail'),(17,'The Kicks','New Rochelle','NY','USA',NULL,'2003-12-03','Ad'),(16,'Today','London','ONT','Canada','www.today.com','2003-10-07','Email'),(18,'21 West Elm','Alamaba','VT','USA','www.21westelm.com','2003-02-05','Ad'),(11,'Highlander','Columbus','OH','USA',NULL,'2002-08-10','Email'),(99,'ELO','Huntington','IN','USA','NULL','2021-11-22','Ad'),(98,'The Foresters','Huntington','IN','USA','NULL','2021-11-22','Ad');
```

```
SQL
-- import/export data notes
-- note: text files can be copied/pasted from MariaDB back to Windows/Mac/Linux
-- j.l. lehman
-- fall 2025

-- see MySQL command line options (from Linux/Windows command line) mysql -?   Or    mysql --help

-- create a table-formatted file
--  -e specifies execute
--  add -N to remove column headings
-- without file redirect "> table.txt" the table is simply displayed
mysql -t -e "select * from Artists" -u lehman -p lehman > table.txt

-- add line numbers to output by piping to cat utility with -n options
mysql -t -e "select * from Artists" -u lehman -p lehman | cat -n

-- Create a tab-delimited file
-- note: tab's may not display correctly unless your redirect to the file or pipe to cat
mysql -e "select * from Artists" -u lehman -p lehman > file.txt

-- Create a HTML file
mysql -H -e "select * from Artists" -u lehman -p lehman > file.html

-- Create a XML file
mysql -X -e "select * from Artists" -u lehman -p lehman > file.xml

-- Create a CSV (Comma Separated Values)
-- tr translates \t to commas
mysql -e "select * from Artists" -u lehman -p lehman | tr "\t" "," > file.csv

-- Backup Database with MySQLDump
-- mysqldump dbname tablename [tablename] -u username -p > file.sql
-- mysqldump --help
mysqldump lehman Artists -u lehman -p > backup.sql

-- CSV to Excel
-- open .csv file in Spreadsheet and it should open/import with no issues, save in Excel format

-- Excel to CSV
-- create a comma delimited file Excel 2016(File, Export, Change File Type, Other File Types, Choose .CSV)

-- Load CSV data into table (from within MySQL)
-- use '\n' only for files created in Linux or Mac
-- ignore removes first line with column headings
-- show warnings after import
-- often need to fix dates in Excel before exporting yyyy-mm-dd ie. 2019-11-17
load data local infile 'test.csv'
into table Artists
fields terminated by ","
optionally enclosed by '"'
lines terminated by '\r\n'
ignore 1 lines;
```
-- end --
