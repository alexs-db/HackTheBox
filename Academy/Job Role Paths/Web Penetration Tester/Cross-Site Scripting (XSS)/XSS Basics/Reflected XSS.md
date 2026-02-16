# Reflected XSS

## Overview

Non-Persistent XSS vulnerabilities come in two types:
- **Reflected XSS**: Processed by the back-end server
- **DOM-based XSS**: Processed entirely on the client-side

Unlike Persistent XSS, these attacks are temporary and don't persist across page refreshes, affecting only the targeted user.

## How Reflected XSS Works

Reflected XSS occurs when user input reaches the back-end server and is returned without filtering or sanitization. Common vectors include:
- Error messages
- Confirmation messages
- Form responses

## Example: Vulnerable To-Do List

Starting with a test input:
```
Input: test
Response: Task 'test' could not be added.
```

If unfiltered, XSS payloads execute:
```html
Input: <script>alert(window.origin)</script>
Response: <div style="padding-left:25px">Task '<script>alert(window.origin)</script>' could not be added.</div>
```

The payload executes in an alert pop-up, but refreshing the page removes it—confirming it's Non-Persistent.

## Targeting Victims

### via GET Requests

Check the HTTP method using Firefox Developer Tools (`CTRL+Shift+I` → Network tab). If a GET request is used, parameters appear in the URL:

1. Send your payload via the application
2. Copy the resulting URL from the address bar
3. Share the malicious URL with victims
4. When victims visit the URL, the XSS payload executes

**Key Point**: The payload persists in the URL, making it shareable for targeted attacks.
