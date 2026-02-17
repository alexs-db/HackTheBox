# Query Results

In this section, we will learn how to control the results output of any query.

## Sorting Results

We can sort the results of any query using `ORDER BY` and specifying the column to sort by:

```sql
SELECT * FROM logins ORDER BY password;
```

| id | username      | password   | date_of_joining         |
|----|---------------|------------|-------------------------|
| 2  | administrator | adm1n_p@ss | 2020-07-02 11:30:50     |
| 3  | john          | john123!   | 2020-07-02 11:47:16     |
| 1  | admin         | p@ssw0rd   | 2020-07-02 00:00:00     |
| 4  | tom           | tom123!    | 2020-07-02 11:47:16     |

By default, the sort is in ascending order, but we can also sort by `ASC` or `DESC`:

```sql
SELECT * FROM logins ORDER BY password DESC;
```

It is also possible to sort by multiple columns for secondary sorting on duplicate values:

```sql
SELECT * FROM logins ORDER BY password DESC, id ASC;
```

## LIMIT Results

To limit large result sets, use `LIMIT` with the number of records needed:

```sql
SELECT * FROM logins LIMIT 2;
```

To add an offset before the limit:

```sql
SELECT * FROM logins LIMIT 1, 2;
```

> **Note:** The offset marks the starting record order (0-indexed). `LIMIT 1, 2` starts at the 2nd record and returns two rows.

## WHERE Clause

Filter specific data using the `WHERE` clause:

```sql
SELECT * FROM table_name WHERE <condition>;
```

**Example:**

```sql
SELECT * FROM logins WHERE id > 1;
```

String and date values must be quoted with `'` or `"`, while numbers don't require quotes.

## LIKE Clause

Use `LIKE` to match patterns in records:

```sql
SELECT * FROM logins WHERE username LIKE 'admin%';
```

- `%` matches zero or more characters
- `_` matches exactly one character

**Example with underscore:**

```sql
SELECT * FROM logins WHERE username LIKE '___';
```

This matches usernames with exactly three characters.
