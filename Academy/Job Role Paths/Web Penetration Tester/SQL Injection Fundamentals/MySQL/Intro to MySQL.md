# Intro to MySQL

This module introduces SQL injection through MySQL. Understanding MySQL and SQL fundamentals is crucial to comprehend how SQL injections work and exploit them effectively.

## Structured Query Language (SQL)

SQL syntax varies between RDBMSs but all must follow the ISO standard. This guide uses MySQL/MariaDB syntax.

SQL enables:
- Retrieve data
- Update data
- Delete data
- Create tables and databases
- Add/remove users
- Assign user permissions

## Command Line

Use the `mysql` utility to authenticate and interact with MySQL/MariaDB. Key flags:
- `-u` for username
- `-p` for password (pass empty to prompt)

```bash
mysql -u root -p
```

**Best practice:** Don't include the password directly to avoid cleartext storage in bash history.

Specify remote hosts and ports with `-h` and `-P` (uppercase for port, lowercase for password):

```bash
mysql -u root -h docker.hackthebox.eu -P 3306 -p
```

The default MySQL/MariaDB port is **3306**.

## Creating a Database

After logging in, use SQL queries to interact with the DBMS. Create a new database with `CREATE DATABASE`:

```sql
CREATE DATABASE users;
```

View databases and switch to one:

```sql
SHOW DATABASES;
USE users;
```

SQL statements are case-insensitive, but database names are case-sensitive. Use uppercase for statements to avoid confusion.

## Tables

DBMS stores data as tables with rows and columns. Each column has a fixed data type (numbers, strings, dates, binary data, etc.).

Create a table with `CREATE TABLE`:

```sql
CREATE TABLE logins (
    id INT,
    username VARCHAR(100),
    password VARCHAR(100),
    date_of_joining DATETIME
);
```

View tables and their structure:

```sql
SHOW TABLES;
DESCRIBE logins;
```

## Table Properties

Key properties for columns:

| Property | Purpose |
|----------|---------|
| `NOT NULL` | Makes field required |
| `UNIQUE` | Ensures unique values |
| `AUTO_INCREMENT` | Auto-increments value |
| `DEFAULT` | Sets default value |
| `PRIMARY KEY` | Uniquely identifies records |

**Complete example:**

```sql
CREATE TABLE logins (
    id INT NOT NULL AUTO_INCREMENT,
    username VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(100) NOT NULL,
    date_of_joining DATETIME DEFAULT NOW(),
    PRIMARY KEY (id)
);
```
