# Code Obfuscation

## Introduction

Before learning about deobfuscation, we must understand code obfuscation. Without this knowledge, we may struggle to successfully deobfuscate code, especially if it uses a custom obfuscator.

## What is Obfuscation?

Obfuscation is a technique that makes scripts difficult for humans to read while maintaining the same technical functionality, though performance may suffer. It's typically automated using obfuscation tools that rewrite code to be much harder to understand.

**Common approach:** Code obfuscators create a dictionary of all words and symbols used, then rebuild the original code during execution by referencing this dictionary.

**Example:** A simple JavaScript code can be obfuscated using tools like [beautifytools.com/javascript-obfuscator.php](http://beautifytools.com/javascript-obfuscator.php)

## Why JavaScript?

Interpreted languages like Python, PHP, and JavaScript publish code without compilation. Python and PHP typically run server-side (hidden from users), but JavaScript executes client-side in the browser, sending code to users in cleartext. This is why obfuscation is commonly used with JavaScript.

## Use Cases

### Legitimate Uses
- **Code protection:** Prevent code reuse and copying without permission
- **Security layer:** Add protection when handling authentication or encryption

> **Note:** Client-side authentication and encryption are not recommended due to increased vulnerability risks.

### Malicious Uses
The most common use of obfuscation is for malicious purposes. Attackers obfuscate malicious scripts to evade detection by Intrusion Detection and Prevention (IDP) systems.
