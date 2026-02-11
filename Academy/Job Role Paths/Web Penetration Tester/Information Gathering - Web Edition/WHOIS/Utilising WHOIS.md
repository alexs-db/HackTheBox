# Utilising WHOIS

## Overview

Let's consider three scenarios to help illustrate the value of WHOIS data.

### Scenario 1: Phishing Investigation

An email security gateway flags a suspicious email sent to multiple employees within a company. The email claims to be from the company's bank and urges recipients to click on a link to update their account information. A security analyst investigates the email and begins by performing a WHOIS lookup on the domain linked in the email.

**WHOIS findings:**
- **Registration Date:** Domain registered just days ago
- **Registrant:** Information hidden behind a privacy service
- **Name Servers:** Associated with a known bulletproof hosting provider

This combination raises significant red flags. The analyst promptly alerts the IT department to block the domain and warns employees.

### Scenario 2: Malware Analysis

A security researcher analyzes a new malware strain communicating with a command-and-control (C2) server. They perform a WHOIS lookup on the C2 domain.

**WHOIS findings:**
- **Registrant:** Individual using a free email service
- **Location:** Country with high cybercrime prevalence
- **Registrar:** History of lax abuse policies

The researcher concludes the C2 server is hosted on a compromised or "bulletproof" server and notifies the hosting provider.

### Scenario 3: Threat Intelligence Report

A cybersecurity firm tracks a sophisticated threat actor group targeting financial institutions and analyzes WHOIS data across multiple domains.

**Patterns identified:**
- Domains registered in clusters before major attacks
- Registrants use various aliases and fake identities
- Domains share the same name servers (common infrastructure)
- Takedown history indicates previous interventions

These insights create a detailed threat actor profile and identify indicators of compromise (IOCs).

---

## Using WHOIS

### Installation

Before using the `whois` command, ensure it's installed:

```bash
alexsdb@htb[/htb]$ sudo apt update
alexsdb@htb[/htb]$ sudo apt install whois -y
```

### Basic Usage Example

Perform a WHOIS lookup on facebook.com:

```bash
alexsdb@htb[/htb]$ whois facebook.com
```

**Sample output:**

```
Domain Name: FACEBOOK.COM
Registry Domain ID: 2320948_DOMAIN_COM-VRSN
Registrar: RegistrarSafe, LLC
Updated Date: 2024-04-24T19:06:12Z
Creation Date: 1997-03-29T05:00:00Z
Registry Expiry Date: 2033-03-30T04:00:00Z
Registrar Abuse Contact Email: abusecomplaints@registrarsafe.com
Name Server: A.NS.FACEBOOK.COM
Name Server: B.NS.FACEBOOK.COM
Name Server: C.NS.FACEBOOK.COM
Name Server: D.NS.FACEBOOK.COM
Registrant Name: Domain Admin
Registrant Organization: Meta Platforms, Inc.
```

### Analysis

**Domain Registration:**
- Registered with RegistrarSafe, LLC since 1997-03-29
- Expiry date: 2033-03-30
- Indicates legitimacy and established presence

**Domain Owner:**
- Organization: Meta Platforms, Inc.
- Contact: Domain Admin

**Domain Status:**
- Protected against unauthorized changes, transfers, and deletions (client and server-side)

**Name Servers:**
- All within facebook.com domain, managed by Meta Platforms, Inc.
- Common practice for large organizations to maintain DNS control

### Key Takeaway

WHOIS data alone may not identify individual employees or specific vulnerabilities. Combine WHOIS findings with other reconnaissance techniques for comprehensive understanding of the target's digital footprint.
