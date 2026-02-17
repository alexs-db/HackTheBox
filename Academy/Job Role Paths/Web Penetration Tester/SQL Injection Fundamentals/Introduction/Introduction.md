# Introduction

Most modern web applications utilize a database structure on the back-end. Such databases store and retrieve data related to the web application, from actual web content to user information and content. To make web applications dynamic, the back-end must interact with the database in real-time. As HTTP(S) requests arrive from users, the application issues queries to the database to build responses. These queries can include information from the HTTP(S) request or other relevant data.

> **Architecture**: A three-tier architecture involves user interaction with a client application (Tier I), which connects to an application server (Tier II), and a DBMS (Tier III).

When user-supplied information constructs database queries, malicious users can exploit the query for unintended purposes through **SQL injection (SQLi)** attacks.

## SQL Injection (SQLi)

SQL injection is one of many injection vulnerabilities in web applications, including HTTP injection, code injection, and command injection. It occurs when a malicious user passes input that changes the final SQL query sent by the web application to the database.

### How SQL Injection Works

1. **Inject SQL code**: Attackers inject code outside expected user input limits (typically using single `'` or double `"` quotes to escape input boundaries)
2. **Subvert logic**: Use SQL syntax to execute both the intended and new queries (via stacked queries or Union queries)
3. **Retrieve output**: Capture or interpret the new query's results on the web application's front-end

## Use Cases and Impact

SQL injection can have tremendous impact, especially with lax back-end privileges:

- **Data theft**: Retrieve sensitive information (logins, passwords, credit card data) leading to account theft and fraud
- **Logic bypass**: Bypass login validation or access admin panels without proper credentials
- **Server compromise**: Read/write files directly on the back-end, place backdoors, and gain control over the website

## Prevention

SQL injections typically result from poorly coded applications or insecure back-end configurations. Mitigation strategies include:

- User input sanitization and validation
- Secure coding practices
- Proper back-end user privileges and access control
