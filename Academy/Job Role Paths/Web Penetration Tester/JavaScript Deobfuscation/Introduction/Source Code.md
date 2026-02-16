# Source Code

Most websites nowadays utilize JavaScript to perform their functions. While HTML determines the website's main fields and parameters, and CSS determines its design, JavaScript performs the necessary functions to run the website. This happens in the background—we only see the pretty front-end and interact with it.

Although all source code is available client-side and rendered by browsers, we often don't pay attention to the HTML source code. However, to understand a page's client-side functionalities, we typically start by examining the page's source code. This section shows how to uncover and understand this code.

## HTML

Start the exercise below, open Firefox in PwnBox, and visit the URL shown in the question:

```
http://SERVER_IP:PORT
Secret Serial Generator: This page generates secret serials.
```

The website displays "Secret Serial Generator" with no input fields or clear functionality. Our next step is to peek at the source code by pressing **Ctrl + U**, which opens the source view:

```
view-source:http://SERVER_IP:PORT
```

HTML source code can contain valuable information, including comments that developers may leave. Always review HTML comments—they may reveal sensitive information.

## CSS

CSS can be defined internally within `<style>` elements or externally in a separate `.css` file referenced in the HTML:

```html
<style>
    *, html {
        margin: 0;
        padding: 0;
        border: 0;
    }
    h1 { font-size: 144px; }
    p { font-size: 64px; }
</style>
```

For external CSS, use the `<link>` tag:

```html
<head>
    <link rel="stylesheet" href="style.css">
</head>
```

## JavaScript

JavaScript can be internally written in `<script>` elements or referenced from an external `.js` file:

```html
<script src="secret.js"></script>
```

When visiting the external script, you may encounter obfuscated code like:

```javascript
eval(function (p, a, c, k, e, d) { e = function (c) { '...SNIP... |true|function'.split('|'), 0, {}))
```

This is **code obfuscation**—a technique that makes code difficult to understand. What is it? How is it done? Where is it used?
