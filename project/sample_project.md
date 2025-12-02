# CS415 Database Sample Project – Fall 2025 - Draft

---

## Database Summary Report

### Project Overview

**Foresters Give** is a small nonprofit that operates out of Huntington University. The group focuses on supporting local service projects, including food drives, campus clean-up days, tutoring events, and community outreach programs. The organization is comprised mostly of HU students, faculty, and alumni who want to give back, either by volunteering or donating money to various campus and community projects.

Each project has its own fundraising goal, purpose, and timeline. Some projects receive a great deal of attention, while others struggle to meet their objectives. Members may choose to donate any amount to any project they care about, and many of them support multiple projects throughout the school year. Currently, Foresters Gives is attempting to manage everything through spreadsheets and emails, which can become messy and lead to errors.

To make things easier and more accurate, **Foresters Give** wants to move to a simple relational database. This database will help keep track of members, projects, and donations in a clear and organized way. It will also allow the group to grow without losing important information or wasting time searching through old files.

### Users View
From a user’s point of view, the database will make everyday tasks much simpler. A staff member or student worker will be able to look up a member’s basic information, view the projects they’ve donated to, and add new donations as they come in. Entering a donation will be as easy as selecting the member, choosing the project, and entering the amount and date.

Project managers will use the database to track the amount of money each project has raised and its proximity to reaching its goal. They can run quick searches to see which projects are doing well and which ones might need more promotion. This will help Foresters Give plan future events and make better decisions about where to focus their efforts.

At the end of the semester or year, the database will facilitate the creation of reports for board meetings or student leadership groups. Reports include information such as total donations, top-giving members, or the most popular projects. Because all the information is stored in one place, the reports will be accurate and easy to generate—something that's hard to do with spreadsheets.

---

## Database ER Model

```mermaid
erDiagram
    MEMBER {
        int mid PK
        varchar first
        varchar last
        varchar title
        varchar city
        char state
        char phone
        varchar email
        date birthdate
        char gender
    }

    PROJECT {
        int pid PK
        varchar name
        text description
        decimal goal
        date start_date
        date end_date
        char status
    }

    DONATION {
        int did PK
        int mid FK
        int pid FK
        decimal amount
        date received
        varchar method
        varchar note
    }

    MEMBER ||--o{ DONATION : makes
    PROJECT ||--o{ DONATION : receives

```

### Database Design Description

The database for Foresters Give is built around three normalized entities: `member`, `project`, and `donation`. Each table stores a focused set of information. Members represent students, faculty, or alumni who participate in donating; projects represent fundraising goals or service initiatives; donations link the two together. Keeping these entities separate avoids repeating information and makes the structure easier to maintain.

During normalization, one major decision was not to copy member names or project names into the donation table. Instead, the donation table stores only foreign keys (mid, pid) and donation-specific details, such as amount and date. This avoids update anomalies—for example, a member changing their email should update one row, not dozens. All fields in each table depend only on the primary key, meaning the design satisfies 3rd Normal Form.

Another design choice was to include a simple status code in the project table rather than placing statuses into a separate lookup table. Since Foresters Give only requires a few basic statuses (such as planned, active, and closed), keeping the field within the project table is both practical and easy for new database students to understand. If needed in the future, this could be expanded into a separate status table.

`member`
The member table stores the personal and contact information for each person who donates to Foresters Give. It acts as the source of truth for names, email addresses, and demographics. All donations must connect back to a member in this table.

`project`
The project table represents each fundraising project or initiative supported by Foresters Give. It contains the project's name, description, fundraising goal, start and end dates, and current status. It lets staff track what projects exist and how active they are.

`donation`
The donation table records each individual donation made by a member to a project. It stores the amount, date, payment method, and any notes. This table is central to all reporting, since totals and summaries come from aggregating donation rows.

---

### Create Tables (20 points)

The following SQL creates the `member`, `project`, and `donation` tables in the current database. Not that it does not create a database, only the tables.

```sql

-- ==========================================
-- MEMBER TABLE
-- Stores people who participate/donate
-- ==========================================
CREATE TABLE member (
    mid       INT            NOT NULL AUTO_INCREMENT,
    first     VARCHAR(20)    NULL,
    last      VARCHAR(25)    NULL,
    title     VARCHAR(10)    NULL,       -- Mr., Ms., Dr., etc.
    city      VARCHAR(25)    NULL,
    state     CHAR(2)        NULL,       -- IN, OH, MI, etc.
    phone     CHAR(10)       NULL,       -- digits only, e.g. 2603594209
    email     VARCHAR(40)    NULL,
    birthdate DATE           NULL,
    gender    CHAR(1)        NULL,       -- M, F, etc.
    PRIMARY KEY (mid)
) ENGINE=InnoDB;

-- ==========================================
-- PROJECT TABLE
-- Stores fundraising projects/initiatives
-- ==========================================
CREATE TABLE project (
    pid         INT            NOT NULL AUTO_INCREMENT,
    name        VARCHAR(40)    NOT NULL,
    description TEXT           NULL,
    goal        DECIMAL(10,2)  NULL,       -- target fundraising goal
    start_date  DATE           NULL,
    end_date    DATE           NULL,
    status      CHAR(1)        NULL,       -- P=planned, A=active, C=closed
    PRIMARY KEY (pid)
) ENGINE=InnoDB;

-- ==========================================
-- DONATION TABLE
-- Links members to projects (who gave what
-- to which project and when)
-- ==========================================
CREATE TABLE donation (
    did       INT            NOT NULL AUTO_INCREMENT,
    mid       INT            NOT NULL,       -- FK to member.mid
    pid       INT            NOT NULL,       -- FK to project.pid
    amount    DECIMAL(10,2)  NOT NULL,
    received  DATE           NOT NULL,
    method    VARCHAR(20)    NULL,           -- cash, card, online, etc.
    note      VARCHAR(100)   NULL,
    PRIMARY KEY (did),
    CONSTRAINT fk_donation_member
        FOREIGN KEY (mid)
        REFERENCES member(mid)
        ON UPDATE RESTRICT
        ON DELETE RESTRICT,
    CONSTRAINT fk_donation_project
        FOREIGN KEY (pid)
        REFERENCES project(pid)
        ON UPDATE RESTRICT
        ON DELETE RESTRICT
) ENGINE=InnoDB;

```

---

### Insert Data (20 points)

Create a single SQL code block to insert data.

* Insert **20–100 rows per table** (more if needed).
* One of your tables must have 100 rows or more of data.

```sql
-- prj2.sql
-- j.l.lehman
-- sample insert statements for CS415 database project
-- adds sample data from exam #3

-- -----------------------------------------------------
-- Data for table `student`
-- -----------------------------------------------------
INSERT INTO `student` (`sid`, `name`) VALUES ('11', 'Alice');
INSERT INTO `student` (`sid`, `name`) VALUES ('22', 'Bob');
INSERT INTO `student` (`sid`, `name`) VALUES ('33', 'Carol');
INSERT INTO `student` (`sid`, `name`) VALUES ('44', 'Dan');


-- -----------------------------------------------------
-- Data for table `camera_type`
-- -----------------------------------------------------
INSERT INTO `camera_type` (`model`, `type`) VALUES ('Canon 90D', 'SLR');
INSERT INTO `camera_type` (`model`, `type`) VALUES ('Nikon D6', 'SLR');
INSERT INTO `camera_type` (`model`, `type`) VALUES ('Canon M20', 'mirrorless');
INSERT INTO `camera_type` (`model`, `type`) VALUES ('Canon A1', 'film');
INSERT INTO `camera_type` (`model`, `type`) VALUES ('Fujifilm 70', 'instant');


-- -----------------------------------------------------
-- Data for table `camera`
-- -----------------------------------------------------
INSERT INTO `camera` (`cid`, `model`) VALUES ('A', 'Canon 90D');
INSERT INTO `camera` (`cid`, `model`) VALUES ('B', 'Canon 90D');
INSERT INTO `camera` (`cid`, `model`) VALUES ('C', 'Nikon D6');
INSERT INTO `camera` (`cid`, `model`) VALUES ('D', 'Canon M20');
INSERT INTO `camera` (`cid`, `model`) VALUES ('E', 'Canon A1');
INSERT INTO `camera` (`cid`, `model`) VALUES ('F', 'Fujifilm 70');

-- -----------------------------------------------------
-- Data for table `loan`
-- -----------------------------------------------------
INSERT INTO `loan` (`lid`, `out`, `returned`, `sid`, `cid`, `days`) VALUES (1, '2019-10-15', TRUE, '11', 'A', 1);
INSERT INTO `loan` (`lid`, `out`, `returned`, `sid`, `cid`, `days`) VALUES (2, '2019-10-15', TRUE, '33', 'B', 2);
INSERT INTO `loan` (`lid`, `out`, `returned`, `sid`, `cid`, `days`) VALUES (3, '2019-10-16', TRUE, '11', 'C', 3);
INSERT INTO `loan` (`lid`, `out`, `returned`, `sid`, `cid`, `days`) VALUES (4, '2019-10-16', FALSE, '44', 'C', 4);
INSERT INTO `loan` (`lid`, `out`, `returned`, `sid`, `cid`, `days`) VALUES (5, '2019-10-18', TRUE, '22', 'D', 2);
INSERT INTO `loan` (`lid`, `out`, `returned`, `sid`, `cid`, `days`) VALUES (6, '2019-10-20', TRUE, '11', 'E', 7);
INSERT INTO `loan` (`lid`, `out`, `returned`, `sid`, `cid`, `days`) VALUES (7, '2019-10-25', FALSE, '33', 'F', 5);

```

---

### Queries (60 points)

Create ten SQL code blocks that demonstrate the following queries. For each query, include a **2–3 sentence description** before 
the SQL code block explaining its purpose and when/why it would be used.  Clear label each Query ie. Query 1, Query 2, etc...  
Show the results of your queries in table format.  Abbreviate the output for large results.

1. `SELECT` using **ORDER BY** two or more columns.

   Show all students sorted by their last name ...
```sql

select * from student order by name desc;

```

2. `SELECT` using a **calculated field** with a meaningful column heading.
   * Example: `lengthseconds / 60 AS minutes` (not an aggregation).
  
   Show loan length as hours ...
         
```sql

select * from days * 24 as hours from loan;

```
  
3. 
4. `SELECT` using a **MariaDB function** (e.g., `MID`, `MONTH`, `DATE`) (not an aggregation).
5. `SELECT` with an **aggregation** (`COUNT`, `SUM`, `MIN`, `AVG`) plus `GROUP BY` and `HAVING`.
6. `Join` of **three or more tables** (INNER JOIN or cross-product).
7. Left or Right `JOIN` (left, or right join).

8. 9. `UPDATE` query.
10. `DELETE` query.
11. Create a `View` and demonstrate using this view.
12. Create a `Transaction` with either `ROLLBACK` or `COMMIT` and demonstrate this transaction.

---

### Reports (20 points) 

Connect to an external reporting tool (or export your data) and create two reports.

1. Chart or Graph-based report
2. Table-based report with Report Title

Use Excel, Access, PowerBI, or any other reporting tool.  Post your report and include a link to each report as a .pdf (or viewable image). 
In one or two paragraphs, describe the reporting software you used and the purpose of each report.

---

### Delete Tables (10 points)

Create a single SQL code block to delete your tables and data.

* Script to delete **all data, tables, and views**.

```sql

-- prj4.sql
-- j.l.lehman
-- sample drop table statements for CS415 database project
-- deletes database tables from exam #3

-- note: must delete tables with foreign keys first
--       to ensure referential integrity

-- drop tables
drop table loan;
drop table camera;
drop table camera_type;
drop table student;
---
```

---

### Poster and Presentation (20 points)

(15 points) Create a poster describing your Database Project using the template provided.  Host poster as .PDF on GitHub, include link to file in your documentation.

[Poster PDF](poster.pdf)


(5 points) Deliver a five-minute presentation during finals that describes your database design, demonstrates your SQL queries, 
and describing any challenges you encountered and insights you gained from the project.


---
  -- end --
  

---
