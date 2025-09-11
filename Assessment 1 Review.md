
# Assessment #1 Review

---

- Exam is on paper-based
- You may use one page front/back 8.5" by 11" of notes on the exam
- Review Practice Exercises and Sample Labs
- Review topics listed under Core Competencies on the course web page

# Core Competencies Covered
- DB-01 – Key database concepts, benefits, relational model basics. (Asse
- DB-02 – Connect to MariaDB/MySQL, navigate databases, list tables, describe structures.
- SQL-01 – Basic SELECT queries: columns, aliases, functions, sorting.
- SQL-02 – Filtering with WHERE, LIKE, IN, BETWEEN, and date functions.
- SQL-03 – Aggregations: SUM, AVG, MIN, MAX, COUNT, GROUP BY, HAVING.

---

Sample SQL Questions/Queries (not an “all-inclusive list”)
---

Note: Use the demo database

Show the SQL needed to perform the following:

1. Update the current user password to be "exam1secret"
2. Display a list of all databases available
3. Choose the database called "demo" and display all tables from this database
4. Display the table structure information (fields, field types, keys) for the table called "member"
5. Display all columns and rows from the table "member"
6. Display all columns and the first two rows from the table "member"

7. Display the last name and state for all records in the member table
8. Display the last name and state for all records in the member table, sorted by ascending last name
9. Display the last name and birthday for all records in the member table, sorted by descending birthday and ascending last name

10. Display all projects that have the letters “er” in the project name.
11. Display all donations made in August of any year
12. Display all donations made in August or April
13. Display all donation amounts and create a calculated column that shows the donation plus 10%

14. Display all donations made during the time period 8-1-2023 to 8-15-2023
15. Display a list of all states from members, removing the duplicates
16. Display the state for each member
17. Display the state and number of members in each state
18. Display the state and number of members in each state that has 3 or more members

19. Generate a greeting for each member in the format “Dear Alice Anderson,” ie. (Dear first last comma)
20. List all members using Last, First format ie. Smith, John sorted by last and first name ascending
21. Generate a standard user login using the first initial and last name ie. NForester for Norman Forester (note: review concat, mid, left, right)

-- end --

