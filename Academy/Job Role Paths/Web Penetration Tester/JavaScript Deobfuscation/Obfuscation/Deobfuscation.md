# Deobfuscation

Now that we understand how code obfuscation works, let's start learning about deobfuscation. Just as there are tools to obfuscate code automatically, there are tools to beautify and deobfuscate code automatically.

## Beautify

The current code is written in a single line, known as **Minified JavaScript code**. To properly format it, we need to beautify our code using:

- **Browser Dev Tools**: In Firefox, press `CTRL+SHIFT+Z` to open the debugger, select your script, and click the `{ }` button to pretty print it.
- **Online tools**: Prettier or Beautifier

Example obfuscated code:
```javascript
eval(function (p, a, c, k, e, d) { e = function (c) { return c.toString(36) }; if (!''.replace(/^/, String)) { while (c--) { d[c.toString(a)] = k[c] || c.toString(a) } k = [function (e) { return d[e] }]; e = function () { return '\\w+' }; c = 1 }; while (c--) { if (k[c]) { p = p.replace(new RegExp('\\b' + e(c) + '\\b', 'g'), k[c]) } } return p }('g 4(){0 5="6{7!}";0 1=8 a();0 2="/9.c";1.d("e",2,f);1.b(3)}', 17, 17, 'var|xhr|url|null|generateSerial|flag|HTB|flag|new|serial|XMLHttpRequest|send|php|open|POST|true|function'.split('|'), 0, {}))
```

> **Note**: Beautifying alone is insufficient because the code is both minified *and* obfuscated. You'll need deobfuscation tools.

## Deobfuscate

Use online tools like **UnPacker** to deobfuscate JavaScript code:
- https://matthewfl.com/unPacker.html

> **Tip**: Ensure no empty lines before the script to avoid inaccurate results.

Deobfuscated output example:
```javascript
function generateSerial() {
    var xhr = new XMLHttpRequest;
    var url = "/serial.php";
    xhr.open("POST", url, true);
    xhr.send(null);
}
```

Alternative: Find the return value at the end and use `console.log` to print it instead of executing it.

## Reverse Engineering

For heavily obfuscated or custom-obfuscated code, automated tools may fail. You'll need to **manually reverse engineer** the code to understand:
- How it was obfuscated
- Its functionality

For advanced JavaScript deobfuscation and reverse engineering techniques, refer to the Secure Coding 101 module.
