# Basic Obfuscation

Code obfuscation is usually not done manually, as there are many tools for various languages that do automated code obfuscation. Many online tools can be found to do so, though many malicious actors and professional developers develop their own obfuscation tools to make it more difficult to deobfuscate.

## Running JavaScript Code

Let us take the following line of code as an example and attempt to obfuscate it:

```javascript
console.log('HTB JavaScript Deobfuscation Module');
```

We can test this code on [JSConsole](https://jsconsole.com) by pasting it and pressing enter. The output shows `HTB JavaScript Deobfuscation Module` printed via the `console.log()` function.

## Minifying JavaScript Code

JavaScript minification reduces code readability while maintaining full functionality by condensing the entire code into a single (often very long) line. This is especially useful for longer code snippets.

Tools like [javascript-minifier](https://javascript-minifier.com/) can help. Simply paste your code and click **Minify** to get the minified output.

Minified JavaScript code is typically saved with the `.min.js` extension.

> **Note:** Code minification is not exclusive to JavaScript and can be applied to many other languages.

## Packing JavaScript Code

To further obfuscate our code, we can use tools like [BeautifyTools](http://beautifytools.com/javascript-obfuscator.php):

```javascript
eval(function(p,a,c,k,e,d){e=function(c){return c};if(!''.replace(/^/,String)){while(c--){d[c]=k[c]||c}k=[function(e){return d[e]}];e=function(){return'\\w+'};c=1};while(c--){if(k[c]){p=p.replace(new RegExp('\\b'+e(c)+'\\b','g'),k[c])}}return p}('5.4(\'3 2 1 0\');',6,6,'Module|Deobfuscation|JavaScript|HTB|log|console'.split('|'),0,{}))
```

This obfuscated code produces the same output when executed on [JSConsole](https://jsconsole.com).

### Packing Details

This obfuscation type is called **"packing"**, recognizable by its six function arguments: `function(p,a,c,k,e,d)`.

A packer converts words and symbols into a dictionary and refers to them using the `(p,a,c,k,e,d)` function to rebuild the original code at runtime. While effective at reducing readability, main strings may still appear in cleartext, potentially revealing functionality. Better obfuscation methods may be needed for sensitive code.
