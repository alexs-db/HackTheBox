# Extensions

Both Burp and ZAP offer extension capabilities, allowing communities to develop plugins that extend functionality. These can perform specific actions on captured requests or add new features like code decoding and beautification.

## Burp Suite: BApp Store

Access extensions via the **Extender** tab and **BApp Store** sub-tab. Extensions can be sorted by popularity.

**Note:** Some extensions are Pro-only; most are available to all users.

### Installing Extensions

Example: **Decoder Improved** extension
- Features: encoding, decoding, hashing, tabs, Unicode support, hex editor
- Dependencies: Some extensions require additional software (e.g., Jython)

Use extensions like you would Burp's native tools. For example, hash text with MD5 or perform other encoding operations.

### Recommended Extensions

| Category | Extensions |
|----------|-----------|
| **Scanning** | Active Scan++, Additional Scanner Checks, Backslash Powered Scanner |
| **Cloud/Infra** | AWS Security Checks, Cloud Storage Tester |
| **Languages** | .NET Beautifier, J2EEScan, Java Deserialization Scanner, PHP Object Injection Check |
| **Analysis** | Headers Analyzer, HTML5 Auditor, JavaScript Security, Retire.JS, CSP Auditor |
| **Utilities** | Random IP Address Header, JS Link Finder, Autorize, CSRF Scanner, Wsdler, Software Version Reporter |

## ZAP: Marketplace

Access add-ons via **Manage Add-ons** → **Marketplace tab**.

Add-ons come in **Release** (stable) or **Beta/Alpha** (experimental) builds.

### Example: FuzzDB Files & Offensive Add-ons

Install popular wordlist collections for fuzzing attacks. Access payloads like OS command injection wordlists to test applications, especially those behind WAFs.

## Closing Thoughts

Both Burp Suite and ZAP are essential for web application penetration testing. Master these alongside Nmap, Hashcat, Wireshark, sqlmap, Ffuf, and Gobuster for comprehensive security assessments.
