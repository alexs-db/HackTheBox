# Mitigating SQL Injection

We have learned about SQL injections, why they occur, and how we can exploit them. We should also learn how to avoid these types of vulnerabilities in our code and patch them when found. Let's look at some examples of how SQL Injection can be mitigated.

## Input Sanitization

Here's the snippet of the code from the authentication bypass section we discussed earlier:

```php
$username = $_POST['username'];
$password = $_POST['password'];

$query = "SELECT * FROM logins WHERE username='". $username. "' AND password = '" . $password . "';" ;
echo "Executing query: " . $query . "<br /><br />";

if (!mysqli_query($conn ,$query)) {
    die('Error: ' . mysqli_error($conn));
}

$result = mysqli_query($conn, $query);
$row = mysqli_fetch_array($result);
```

The script takes in the username and password from the POST request and passes it to the query directly. This allows attackers to inject malicious code. Injection can be avoided by sanitizing any user input using functions like `mysqli_real_escape_string()`, which escapes special characters such as `'` and `"`.

```php
$username = mysqli_real_escape_string($conn, $_POST['username']);
$password = mysqli_real_escape_string($conn, $_POST['password']);

$query = "SELECT * FROM logins WHERE username='". $username. "' AND password = '" . $password . "';" ;
echo "Executing query: " . $query . "<br /><br />";
```

The injection no longer works due to escaping the single quotes. Similar functions include `pg_escape_string()` for PostgreSQL queries.

## Input Validation

User input can also be validated based on expected data format. For example, email inputs can be validated against the pattern `...@email.com`.

```php
<?php
if (isset($_GET["port_code"])) {
    $q = "Select * from ports where port_code ilike '%" . $_GET["port_code"] . "%'";
    $result = pg_query($conn,$q);
    
    if (!$result) {
        die("</table></div><p style='font-size: 15px;'>" . pg_last_error($conn). "</p>");
    }
}
?>
```

Since port codes consist only of letters or spaces, we can restrict input using a regular expression:

```php
$pattern = "/^[A-Za-z\s]+$/";
$code = $_GET["port_code"];

if(!preg_match($pattern, $code)) {
    die("</table></div><p style='font-size: 15px;'>Invalid input! Please try again.</p>");
}

$q = "Select * from ports where port_code ilike '%" . $code . "%'";
```

The `preg_match()` function validates that input matches the pattern `[A-Za-z\s]+`. Any other character terminates the script.

## User Privileges

Ensure that database users have minimum permissions. Never use superusers or administrative accounts with web applications.

```sql
CREATE USER 'reader'@'localhost';
GRANT SELECT ON ilfreight.ports TO 'reader'@'localhost' IDENTIFIED BY 'p@ssw0Rd!!';
```

This creates a user with SELECT-only privileges on the ports table:

```sql
mysql -u reader -p
USE ilfreight;
SELECT * FROM ilfreight.credentials;
-- ERROR 1142 (42000): SELECT command denied
```

## Web Application Firewall

Web Application Firewalls (WAF) detect malicious input and reject suspicious HTTP requests. Examples include ModSecurity (open-source) and Cloudflare (premium). They reject requests containing common SQL injection patterns like `INFORMATION_SCHEMA`.

## Parameterized Queries

Parameterized queries use placeholders for input data, ensuring safe escaping:

```php
$username = $_POST['username'];
$password = $_POST['password'];

$query = "SELECT * FROM logins WHERE username=? AND password = ?" ;
$stmt = mysqli_prepare($conn, $query);
mysqli_stmt_bind_param($stmt, 'ss', $username, $password);
mysqli_stmt_execute($stmt);
$result = mysqli_stmt_get_result($stmt);

$row = mysqli_fetch_array($result);
mysqli_stmt_close($stmt);
```

The placeholders `?` are safely filled using `mysqli_stmt_bind_param()`.

## Conclusion

These mitigation techniques apply across all common languages and libraries. However, exploitation may still be possible based on application logic.
