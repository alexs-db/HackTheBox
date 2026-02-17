# SQL Statements

Now that we understand how to use the mysql utility and create databases and tables, let us look at some of the essential SQL statements and their uses.

## INSERT Statement

The INSERT statement is used to add new records to a given table. The statement following the below syntax:

```sql
INSERT INTO table_name VALUES (column1_value, column2_value, column3_value, ...);
```

The syntax above requires the user to fill in values for all the columns present in the table.

```
mysql> INSERT INTO logins VALUES(1, 'admin', 'p@ssw0rd', '2020-07-02');
Query OK, 1 row affected (0.00 sec)
```

We can skip filling columns with default values by specifying column names:

```sql
INSERT INTO table_name(column2, column3, ...) VALUES (column2_value, column3_value, ...);
```

```
mysql> INSERT INTO logins(username, password) VALUES('administrator', 'adm1n_p@ss');
Query OK, 1 row affected (0.00 sec)
```

> **Note:** Skipping columns with the 'NOT NULL' constraint will result in an error. Also, the examples use cleartext passwords for demonstration only—passwords should always be hashed/encrypted before storage.

Insert multiple records at once:

```
mysql> INSERT INTO logins(username, password) VALUES ('john', 'john123!'), ('tom', 'tom123!');
Query OK, 2 rows affected (0.00 sec)
```

## SELECT Statement

The SELECT statement retrieves data from tables. View the entire table:

```sql
SELECT * FROM table_name;
```

The asterisk (*) selects all columns. Select specific columns:

```sql
SELECT column1, column2 FROM table_name;
```

```
mysql> SELECT * FROM logins;
+----+---------------+------------+---------------------+
| id | username      | password   | date_of_joining     |
+----+---------------+------------+---------------------+
|  1 | admin         | p@ssw0rd   | 2020-07-02 00:00:00 |
|  2 | administrator | adm1n_p@ss | 2020-07-02 11:30:50 |
|  3 | john          | john123!   | 2020-07-02 11:47:16 |
|  4 | tom           | tom123!    | 2020-07-02 11:47:16 |
+----+---------------+------------+---------------------+
4 rows in set (0.00 sec)

mysql> SELECT username, password FROM logins;
+---------------+------------+
| username      | password   |
+---------------+------------+
| admin         | p@ssw0rd   |
| administrator | adm1n_p@ss |
| john          | john123!   |
| tom           | tom123!    |
+---------------+------------+
4 rows in set (0.00 sec)
```

## DROP Statement

Remove tables and databases:

```
mysql> DROP TABLE logins;
Query OK, 0 rows affected (0.01 sec)

mysql> SHOW TABLES;
Empty set (0.00 sec)
```

> **Warning:** DROP permanently deletes the table with no confirmation—use with caution.

## ALTER Statement

ALTER changes table names, fields, and columns:

```
mysql> ALTER TABLE logins ADD newColumn INT;
Query OK, 0 rows affected (0.01 sec)
```

Rename a column:

```
mysql> ALTER TABLE logins RENAME COLUMN newColumn TO newerColumn;
Query OK, 0 rows affected (0.01 sec)
```

Change a column's datatype:

```
mysql> ALTER TABLE logins MODIFY newerColumn DATE;
Query OK, 0 rows affected (0.01 sec)
```

Drop a column:

```
mysql> ALTER TABLE logins DROP newerColumn;
Query OK, 0 rows affected (0.01 sec)
```

## UPDATE Statement

UPDATE modifies specific records based on conditions:

```sql
UPDATE table_name SET column1=newvalue1, column2=newvalue2, ... WHERE <condition>;
```

```
mysql> UPDATE logins SET password = 'change_password' WHERE id > 1;
Query OK, 3 rows affected (0.00 sec)

mysql> SELECT * FROM logins;
+----+---------------+-----------------+---------------------+
| id | username      | password        | date_of_joining     |
+----+---------------+-----------------+---------------------+
|  1 | admin         | p@ssw0rd        | 2020-07-02 00:00:00 |
|  2 | administrator | change_password | 2020-07-02 11:30:50 |
|  3 | john          | change_password | 2020-07-02 11:47:16 |
|  4 | tom           | change_password | 2020-07-02 11:47:16 |
+----+---------------+-----------------+---------------------+
4 rows in set (0.00 sec)
```

> **Note:** Always include the WHERE clause to specify which records to update.
