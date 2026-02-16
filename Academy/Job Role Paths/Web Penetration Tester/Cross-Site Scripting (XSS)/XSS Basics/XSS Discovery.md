# XSS Discovery

## Overview

We've covered XSS vulnerability types and how JavaScript injection executes in the client-side. This section explores detection methods for XSS vulnerabilities within web applications. While detection can be as challenging as exploitation, numerous tools exist to assist in identifying XSS issues.

## Automated Discovery

### Web Application Vulnerability Scanners

Tools like Nessus, Burp Pro, and ZAP use two scanning approaches:

- **Passive Scan**: Reviews client-side code for potential DOM-based vulnerabilities
- **Active Scan**: Injects various payloads to trigger XSS through source injection

### Open-Source Tools

Popular open-source alternatives include **XSS Strike**, **Brute XSS**, and **XSSer**. These tools identify input fields, send XSS payloads, and compare rendered page sources for successful injections.

#### Using XSS Strike

```bash
git clone https://github.com/s0md3v/XSStrike.git
cd XSStrike
pip install -r requirements.txt
python xsstrike.py -u "http://SERVER_IP:PORT/index.php?task=test"
```

**Note**: Always manually verify automated findings, as payloads may be injected without successful execution.

## Manual Discovery

### XSS Payloads

The basic approach tests various payloads against input fields. Resources like [PayloadAllTheThings](https://github.com/swisskyrepo/PayloadAllTheThings) and [Payload-Box](https://github.com/Payload-Box) maintain extensive payload lists.

**Important**: Many payloads won't work because they're designed for specific injection contexts (e.g., after quotes) or security bypass scenarios.

> **Note**: XSS can be injected into any HTML input, including HTTP headers (Cookie, User-Agent) when displayed on the page.

For efficiency, consider automating payload testing with custom Python scripts rather than manual copy-pasting, especially with multiple input fields.

### Code Review

The most reliable detection method is **manual code review** of both back-end and front-end code. Understanding how input flows from source to browser enables crafting custom payloads with high confidence.

Common web applications likely patch vulnerabilities detected by automated tools. Manual code review may reveal undetected XSS in public releases.

For advanced techniques, see **Secure Coding 101: JavaScript** and **Whitebox Pentesting 101: Command Injection** modules.
