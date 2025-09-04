# CS415 Database Management
## Fall 2025  
### Practice Exercise #1 – DB-02  

---

## MariaDB Essential Commands

### Web Client
Use **phpMyAdmin** to connect to the MariaDB server hosted on `ada.huntington.edu`.

- **Username**: your last name (all lowercase)  
  Example: `smith`  
- **Password**: `cs415` (all lowercase)  

🔗 [phpMyAdmin on Ada](https://ada.huntington.edu/phpmyadmin/)

➡️ In phpMyAdmin, click the **SQL** tab, enter commands, and press **Go**.

---

### Basic Commands

#### See database version
```sql
select version();
````

#### Show available databases

```sql
show databases;
```

#### Select a database

```sql
use demo;
```

#### List tables in the database

```sql
show tables;
```

#### Show table structure

```sql
describe student;
desc student;
```

#### Full table structure (with extra options)

```sql
show create table student;
```

---

### Viewing Data

#### Show all data in table format

```sql
select * from student;
```

#### Limit results (first X rows)

```sql
select * from student limit 5;
```

#### Choose specific columns

```sql
select first_name, last_name from student;
```

---

### Account Management

#### Change your database account password

```sql
set password = password("new_password");
```

#### See users and passwords (admin only)

```sql
use mysql;
select user, host, passwd from user;
```

---

### Logout

In phpMyAdmin, click the **Logout** button (to the right of the Home button).

---

*Last modified: Tuesday, August 26, 2025, 11:18 AM*

```

---

