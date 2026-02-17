# Subverting Query Logic

Now that we have a basic idea about how SQL statements work, let us get started with SQL injection. Before we start executing entire SQL queries, we will first learn to modify the original query by injecting the OR operator and using SQL comments to subvert the original query's logic. A basic example of this is bypassing web authentication, which we will demonstrate in this section.

## Authentication Bypass

Consider the following administrator login page:

- Admin panel login form with fields for Username and Password, and a Login button

We can log in with the administrator credentials `admin / p@ssw0rd`.

The page displays the SQL query being executed:

```sql
SELECT * FROM logins WHERE username='admin' AND password='p@ssw0rd';
```

The page takes in the credentials, then uses the AND operator to select records matching the given username and password. If the MySQL database returns matched records, the credentials are valid. Let us see what happens when we enter incorrect credentials.

When entering incorrect credentials, the login fails due to the wrong password leading to a false result from the AND operation.

## SQLi Discovery

Before we start subverting the web application's logic, we first have to test whether the login form is vulnerable to SQL injection. Try one of the below payloads after the username:

| Payload | URL Encoded |
|---------|-------------|
| `'` | `%27` |
| `"` | `%22` |
| `#` | `%23` |
| `;` | `%3B` |
| `)` | `%29` |

**Note:** Use the URL encoded version when putting payloads directly in the URL (HTTP GET request).

Let us start by injecting a single quote:

```sql
SELECT * FROM logins WHERE username=''' AND password = 'something';
```

This causes a SQL syntax error because the quotes are unbalanced. One solution is to comment out the rest of the query or use an even number of quotes.

## OR Injection

To bypass authentication, we need the query to always return true. We can abuse the OR operator since AND is evaluated before OR in SQL.

A condition that always returns true is `'1'='1'`. Using `admin' or '1'='1` as the username keeps the quotes balanced:

```sql
SELECT * FROM logins WHERE username='admin' or '1'='1' AND password = 'something';
```

**Query Logic:**
- AND is evaluated first: `'1'='1'` (True) AND `password='something'` (False) = False
- OR is evaluated next: `username='admin'` (True) OR False = **True**

This successfully logs in as admin.

### Bypassing With Unknown Username

If the username is unknown, we inject OR into the password field:

```sql
SELECT * FROM logins WHERE username='' OR '1'='1' AND password='' OR '1'='1';
```

This returns true regardless of username and password, logging in with the first user in the table.

**Note:** For a comprehensive list of SQLi auth bypass payloads, see [PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings).
