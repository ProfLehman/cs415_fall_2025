# CS415 Database Project – Fall 2025

**Due Date:** Monday, December 8th at 5:00 pm. (Extended from Tuesday 12/2)

**Presentations:** Final Exam period

**Points:** 200 points (20% of your grade)

## Overview

For your database project, you will design and implement a relational database in **MariaDB** that addresses a meaningful real-world problem. 
You may choose a project connected to a business, organization, club, ministry, or personal interest. 
Your database should model a realistic data set (with fictitious sample data to protect privacy) and demonstrate the skills developed in this course, including:

* ER modeling
* Normalization
* Table creation
* Data manipulation
* SQL queries
* Security
* Reporting

This project offers you the opportunity to integrate the **Core Competencies** and **Applied Labs** into a comprehensive solution that showcases both your technical and design abilities.

## Submitting your project

All project code and documentation must be hosted on Github using Markdown for formatting and SQL code blocks.

Note: Make sure you **commit changes** as you create your documentation.  Each time you commit you are creating a point at which you can "revert" or "undo" your changes.  Also, following the best **3:2:1 backup strategies**, you should create two backup copies of your project, ie, copy to the local drive and copy to the cloud.

---
## Requirements

### Database Summary Report (10 points)

* 2 or 3 paragraphs describing the business/organization/person that will use your database.
* 2 or 3 paragraphs describing how the database will be used from a user’s perspective.

---

### Database ER Model (40 points)

* Fully normalized (or provide explanation for denormalization).
* Using `Mermaid` show your ER diagram including MariaDB data types, primary keys, foreign keys,
* relationships (with names), and participation.
* 2 or 3 paragraphs describing the overall design for your database, including any issues or design choices you made as part of the normalization process.
* 2 or 3 sentences each describing the purpose of each table in your database.

---

### Create Tables (20 points)

Create a single SQL code block to create your tables.

* Create **3–5 tables** (more if needed).
* Each table has **3–10 fields**.
* Use **4 or more MariaDB data types**.
* Include **primary keys** and **foreign keys** for each table.
* Include indexes as appropriate.
* Do **not** include a `CREATE DATABASE` statement in your script.


### Insert Data (20 points)

Create a single SQL code block to insert data.

* Insert **20–100 rows per table** (more if needed).
* One of your tables must have 100 rows or more of data.


### Queries (60 points)

Create ten SQL code blocks that demonstrate the following queries. For each query, include a **2–3 sentence description** before 
the SQL code block explaining its purpose and when/why it would be used.  Clear label each Query ie. Query 1, Query 2, etc...  
Show the results of your queries in table format.  Abbreviate the output for large results.

1. `SELECT` using **ORDER BY** two or more columns.
2. `SELECT` using a **calculated field** with a meaningful column heading.
   * Example: `lengthseconds / 60 AS minutes` (not an aggregation).
3. `SELECT` using a **MariaDB function** (e.g., `MID`, `MONTH`, `DATE`) (not an aggregation).
4. `SELECT` with an **aggregation** (`COUNT`, `SUM`, `MIN`, `AVG`) plus `GROUP BY` and `HAVING`.
5. `Join` of **three or more tables** (INNER JOIN or cross-product).
6. Left or Right `JOIN` (left, or right join).
7. `UPDATE` query.
9. `DELETE` query.
10. Create a `View` and demonstrate using this view.
11. Create a `Transaction` with either `ROLLBACK` or `COMMIT` and demonstrate this transaction.


### Reports (20 points) 

Connect to an external reporting tool (or export your data) and create two reports.

1. Chart or Graph-based report
2. Table-based report with Report Title

Use Excel, Access, PowerBI, or any other reporting tool.  Post your report and include a link to each report as a .pdf (or viewable image). 
In one or two paragraphs, describe the reporting software you used and the purpose of each report.


### Delete Tables (10 points)

Create a single SQL code block to delete your tables and data.

* Script to delete **all data, tables, and views**.

---

### Poster and Presentation (20 points)

(15 points) Create a poster describing your Database Project using the template provided.  Host poster as .PDF on GitHub, include link to file in your documentation.

(5 points) Deliver a five-minute presentation during finals that describes your database design, demonstrates your SQL queries, 
and describing any challenges you encountered and insights you gained from the project.

---


## Final Notes
* All SQL code blocks must work if executed in this order ie. create tables, insert data, queries, delete tables
* **10% project grade deduction for script errors**. Test your code! Have another student test your scripts.
* The project represents **20% of your final grade**.
* Start early, ask questions, and do your best!

  -- end --
  

---
