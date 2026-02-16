# Stored XSS

## Overview

**Stored XSS** (also called Persistent XSS) is the most critical type of XSS vulnerability. When an injected payload is stored in the backend database and retrieved when visiting the page, it becomes persistent and affects any user who visits that page.

### Why It's Critical

- Affects a wider audience (all visiting users)
- May be difficult to remove (requires backend database cleanup)
- More severe than other XSS types

## Testing Stored XSS

### Example: To-Do List Application

Start the server to practice:
```
http://SERVER_IP:PORT/
```

1. Type a test item and press Enter
2. Observe how the page handles your input

### Basic XSS Payload

To test vulnerability, use:

```html
<script>alert(window.origin)</script>
```

**Why this payload?**
- Easy to identify when executed
- Shows the page URL in the alert
- Useful for detecting IFrame usage (modern security measure)

### Confirming the Vulnerability

1. **Check if payload executes** → Alert displays the page URL
2. **Verify persistence** → Refresh the page
3. **Confirm vulnerability** → If alert appears after refresh, it's Stored XSS

View page source (`CTRL+U`) to see the stored payload:
```html
<div></div><ul class="list-unstyled" id="todo"><ul><script>alert(window.origin)</script></ul></ul>
```

## Alternative Testing Payloads

If `alert()` is blocked, try:

- **`<plaintext>`** - Stops HTML rendering, displays remaining code as text
- **`<script>print()</script>`** - Opens browser print dialog (rarely blocked)

> **Tip:** Modern browsers may block `alert()` in certain contexts. Always test multiple payloads to confirm XSS existence.
