# Fingerprinting

Fingerprinting focuses on extracting technical details about the technologies powering a website or web application. Similar to how a fingerprint uniquely identifies a person, the digital signatures of web servers, operating systems, and software components can reveal critical information about a target's infrastructure and potential security weaknesses.

## Why Fingerprinting Matters

- **Targeted Attacks**: Exploit vulnerabilities specific to identified technologies
- **Identifying Misconfigurations**: Expose outdated software, default settings, and weaknesses
- **Prioritising Targets**: Focus efforts on systems more likely to be vulnerable
- **Building Profiles**: Create a holistic view of the target's security posture

## Fingerprinting Techniques

| Technique | Description |
|-----------|-------------|
| Banner Grabbing | Analyse server banners for software, versions, and details |
| HTTP Headers | Extract information from Server, X-Powered-By, and other headers |
| Probing Responses | Send crafted requests to elicit revealing responses |
| Content Analysis | Examine page structure, scripts, and copyright headers |

## Common Fingerprinting Tools

| Tool | Description |
|------|-------------|
| **Wappalyzer** | Browser extension for technology profiling |
| **BuiltWith** | Detailed technology stack reports |
| **WhatWeb** | Command-line tool with signature database |
| **Nmap** | Network scanner with fingerprinting capabilities |
| **Netcraft** | Web security and hosting analysis |
| **wafw00f** | Identifies Web Application Firewalls (WAFs) |

## Case Study: inlanefreight.com

### Banner Grabbing

```bash
curl -I inlanefreight.com
```

**Findings**: Apache/2.4.41 (Ubuntu), WordPress redirect detected

```bash
curl -I https://www.inlanefreight.com
```

**Output**: WordPress confirmation via `wp-json` paths and Link headers

### WAF Detection (wafw00f)

```bash
wafw00f inlanefreight.com
```

**Result**: **Wordfence WAF** (by Defiant) detected - security layer present

### Vulnerability Assessment (Nikto)

```bash
nikto -h inlanefreight.com -Tuning b
```

**Key Findings**:
- **Server**: Apache/2.4.41 (Ubuntu) - outdated
- **CMS**: WordPress installation with accessible `/wp-login.php`
- **IPs**: 134.209.24.248 (IPv4), 2a03:b0c0:1:e0::32c:b001 (IPv6)
- **Security Issues**: Missing HSTS header, insecure cookies, no X-Content-Type-Options
- **Files**: `license.txt` discoverable

### Reconnaissance Summary

The target runs a WordPress site on outdated Apache, protected by Wordfence WAF. Multiple security misconfigurations identified, making it a potential target for WordPress exploits.
