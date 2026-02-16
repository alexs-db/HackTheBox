# XSS Prevention

We now understand XSS vulnerabilities, their types, detection methods, and exploitation techniques. This section covers defensive strategies against XSS attacks.

XSS vulnerabilities stem from two key points: a **Source** (user input) and a **Sink** (output display). Securing both is essential across front-end and back-end layers.

## Core Prevention Principles

- **Input sanitization and validation** on both front-end and back-end
- **Output encoding** to safely display user data
- **Server-side security configurations**

---

## Front-End Protection

### Input Validation

Validate input format before submission using regex patterns:

```javascript
function validateEmail(email) {
    const re = /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    return re.test($("#login input[name=email]").val());
}
```

### Input Sanitization

Use **DOMPurify** to escape special characters and prevent DOM XSS:

```javascript
<script src="dist/purify.min.js"></script>
let clean = DOMPurify.sanitize(dirty);
```

### Avoid Dangerous Patterns

Never place user input directly in:
- `<script>` tags
- `<style>` tags
- HTML attributes: `<div name='INPUT'></div>`
- HTML comments: `<!-- -->`

Avoid these DOM manipulation methods:
- `innerHTML`, `outerHTML`
- `document.write()`, `document.writeln()`
- jQuery: `html()`, `append()`, `prepend()`, `after()`, etc.

---

## Back-End Protection

### Input Validation

Validate input server-side using language-specific functions:

**PHP:**
```php
if (filter_var($_GET['email'], FILTER_VALIDATE_EMAIL)) {
    // process
} else {
    // reject input
}
```

**Node.js:** Use the same approaches as front-end validation.

### Input Sanitization

Escape special characters server-side (front-end sanitization can be bypassed):

**PHP:**
```php
addslashes($_GET['email'])
```

**Node.js:**
```javascript
import DOMPurify from 'dompurify';
var clean = DOMPurify.sanitize(dirty);
```

### Output Encoding

Encode special characters to HTML entities before display:

**PHP:**
```php
htmlentities($_GET['email']);
```

**Node.js:**
```javascript
import encode from 'html-entities';
encode('<'); // → '&lt;'
```

---

## Server Configuration

Implement security headers and settings:

- **HTTPS** across all domains
- **X-Content-Type-Options**: `nosniff`
- **Content-Security-Policy**: `script-src 'self'` (local scripts only)
- **Cookie flags**: `HttpOnly` and `Secure`
- **Web Application Firewall (WAF)** to detect and block injection attacks
- Framework-level protections (e.g., ASP.NET built-in XSS defense)

---

## Summary

Effective XSS prevention requires:
1. Input validation and sanitization (front & back-end)
2. Output encoding
3. Secure server configuration
4. Continuous security testing and vulnerability assessment

Combine offensive and defensive techniques to maintain strong XSS protection.
