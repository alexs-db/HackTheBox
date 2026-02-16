# DOM XSS

## Overview

DOM-based XSS (Non-Persistent) is processed entirely on the client-side through JavaScript, unlike reflected XSS which sends data to the backend. It occurs when JavaScript changes the page source via the Document Object Model (DOM).

## Example: Vulnerable To-Do List

Running the server below demonstrates a DOM XSS vulnerability:

```
http://SERVER_IP:PORT/
```

Key observations:
- URL uses a hashtag `#` parameter (client-side only)
- Network tab shows **no HTTP requests** are made
- Page source (`CTRL+U`) doesn't contain user input
- Rendered source (`CTRL+SHIFT+C`) shows the injected content
- Input persists only until page refresh (Non-Persistent)

## Source & Sink

**Source**: JavaScript object that captures user input (URL parameters, input fields, etc.)

**Sink**: Function that writes user input to DOM objects. Common vulnerable sinks:

```javascript
// Native JavaScript
document.write()
DOM.innerHTML
DOM.outerHTML

// jQuery functions
add()
after()
append()
```

Unsanitized sinks are vulnerable to XSS attacks.

### Vulnerable Code Example

From `script.js`:

```javascript
var pos = document.URL.indexOf("task=");
var task = document.URL.substring(pos + 5, document.URL.length);
document.getElementById("todo").innerHTML = "<b>Next Task:</b> " + decodeURIComponent(task);
```

The input is directly written without sanitization.

## DOM XSS Attacks

`<script>` tags are blocked by `innerHTML`, but other payloads work:

```html
<img src="" onerror=alert(window.origin)>
```

This creates an image element with an `onerror` handler that executes when the image fails to load (empty `src`).

**Example exploitation:**
```
http://SERVER_IP:PORT/#task=<img src="" onerror=alert(window.origin)>
```

Share this URL with a target user to execute the JavaScript payload.
