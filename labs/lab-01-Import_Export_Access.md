# CS 415 Database Management Systems 
## Lab-01 – Import/Export - 40 Points
## Recommended Due: 13 November 2025 (Final Due:  04 December 2025 at 5 pm.)

---

The purpose of this assignment is to learn how to import and export data with MariaDB.

We will be using Microsoft Access (Windows only) for this assignment. You can use Microsoft Access in the Computer Labs (S175/177).

See [office Portal](https://portal.office.com) to download Access on a Windows computer.

Pick a **single table** from your final project to complete Parts 1 to 4.

### Part 1.  Backup Database
Save a copy of your table create and insert statements using mysqldump in a file called lab1.sql

### Part 2.  Comma-Delimited (CSV – comma-separated values)
Save the table as a comma-delimited file called lab1.csv

### Part 3.  CSV to Excel
Import your file from Part 2 into Excel and save the file (in Excel format) as lab1.xlsx

### Part 4.  Microsoft Access

1. Create an **Access database** called `lab1.accdb`

2. Create and save a **query to create your table** in Access

3. Copy and **paste your data from the Excel Spreadsheet** (Part 3 of this assignment) into your table

4. Create and save **two sample queries** for your table

5. Create and save **two sample reports** for your table

#### Submitting your assignment

Upload a zip file called `lab1.zip` of the following four files.
    1. lab1.sql
    2. lab1.csv
    3. lab1.xlsx
    4. lab1.accdb

-- end assignment --


---

## Import/Export Notes and Class Examples

Text files can be copied/pasted from MariaDB back to Windows/Mac/Linux.  
Note: See SQL below for sample `artists` table used in these examples.


### MariaDB/Mysql command line options (from Linux/Windows command line) 

```SQL

mariadb -?   
mariadb --help
```

### Create an ASCII table-formatted file

-t = table output  
-e = execute  
add -N to remove column headings  
without file redirect "> table.txt" the table is simply displayed

```sql
mariadb -t -e "select * from artists" -u fisher -p fisher > table.txt
```

Note: to see files created type `ls` to see files, then 'cat filename` to display file.

```BASH
ls
cat table.txt
```


### Add line numbers to output

Use the `cat` utility with the `-n` option to display line numbers in the query output.

```sql
mariadb -t -e "select * from artists" -u fisher -p fisher | cat -n
```


### Create a tab-delimited file

Tabs may not display correctly unless redirected to a file or piped to `cat`.

```sql
mariadb -e "select * from artists" -u fisher -p fisher > file.txt
```


### Create an HTML file

Use the `-H` flag to output results as an HTML table.

```sql
mariadb -H -e "select * from artists" -u fisher -p fisher > file.html
```


### Create an XML file

Use the `-X` flag to output results in XML format.

```sql
mariadb -X -e "select * from artists" -u fisher -p fisher > file.xml
```


### Create a CSV (comma-separated values) file

Use `tr` to translate tabs into commas.

```bash
mariadb -e "select * from artists" -u fisher -p fisher | tr "\t" "," > file.csv
```


### Backup database with `mysqldump`

`mysqldump` creates a `.sql` script that can recreate the table and its data.

```bash
mysqldump fisher artists -u fisher -p > backup.sql
```

**Notes:**

* Syntax: `mysqldump dbname tablename [tablename] -u username -p > file.sql`
* Run `mysqldump --help` for more options.


--- 
### CSV to Excel

Open the `.csv` file in a spreadsheet application such as Excel. It should import cleanly.
You can then **Save As → Excel Workbook (.xlsx)** if desired.

---

### Excel to CSV

From Excel:
**File → Export / Save As → Choose File Type → CSV (Comma delimited) (.csv)**


### Load CSV data into table for Windows: terminated by \r\n

Import CSV data from within MariaDB/MySQL.  
Use `\n` for Linux/Mac line endings or `\r\n` for Windows.  
`ignore 1 lines` skips the header row.  

```sql
load data local infile 'test.csv'
into table artists
fields terminated by ','
optionally enclosed by '"'
lines terminated by '\r\n'
ignore 1 lines
(artist_id, artist_name, city, region, country, web_address, entry_date, lead_source);
```

### Load CSV data into table for Linux/Mac files: terminated by \n

```sql
load data local infile 'test.csv'
into table artists
fields terminated by ','
optionally enclosed by '"'
lines terminated by '\n'
ignore 1 lines
(artist_id, artist_name, city, region, country, web_address, entry_date, lead_source);
```


---

### Create statement for sample artists table
```sql

CREATE TABLE artists (
  artist_id int(11) NOT NULL,
  artist_name varchar(50) NOT NULL,
  city varchar(25) DEFAULT NULL,
  region varchar(15) DEFAULT NULL,
  country varchar(20) DEFAULT NULL,
  web_address varchar(40) DEFAULT NULL,
  entry_date date DEFAULT NULL,
  lead_source varchar(10) DEFAULT NULL
) ENGINE=InnoDB;

```

### Insert for sample artists table
```sql

INSERT INTO artists (artist_id, artist_name, city, region, country, web_address, entry_date, lead_source)
VALUES
(1,'The Neurotics','Peterson','NC','USA','www.theneurotics.com','2003-05-14','Directmail'),
(2,'Louis Holiday','Clinton','IL','USA',NULL,'2003-06-03','Directmail'),
(3,'Word','Anderson','IN','USA',NULL,'2003-06-08','Email'),
(5,'Sonata','Alexandria','VA','USA','www.classical.com/sonata','2003-06-08','Ad'),
(10,'The Bullets','Alverez','TX','USA',NULL,'2003-08-10','Email'),
(14,'Jose MacArthur','Santa Rosa','CA','USA','www.josemacarthur.com','2003-08-17','Ad'),
(15,'Confused','Tybee Island','GA','USA',NULL,'2003-09-14','Directmail'),
(17,'The Kicks','New Rochelle','NY','USA',NULL,'2003-12-03','Ad'),
(16,'Today','London','ONT','Canada','www.today.com','2003-10-07','Email'),
(18,'21 West Elm','Alamaba','VT','USA','www.21westelm.com','2003-02-05','Ad'),
(11,'Highlander','Columbus','OH','USA',NULL,'2002-08-10','Email'),
(99,'ELO','Huntington','IN','USA',NULL,'2021-11-22','Ad'),
(98,'The Foresters','Huntington','IN','USA',NULL,'2021-11-22','Ad');

```

-- end notes --
