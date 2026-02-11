# WHOIS

## Overview

WHOIS is a widely used query and response protocol designed to access databases that store information about registered internet resources. Primarily associated with domain names, WHOIS can also provide details about IP address blocks and autonomous systems. Think of it as a giant phonebook for the internet, letting you look up who owns or is responsible for various online assets.

## Example Query

```bash
alexsdb@htb[/htb]$ whois inlanefreight.com
```

**Sample Output:**
```
Domain Name: inlanefreight.com
Registry Domain ID: 2420436757_DOMAIN_COM-VRSN
Registrar WHOIS Server: whois.registrar.amazon
Registrar URL: https://registrar.amazon.com
Updated Date: 2023-07-03T01:11:15Z
Creation Date: 2019-08-05T22:43:09Z
```

## WHOIS Record Components

- **Domain Name:** The domain itself (e.g., example.com)
- **Registrar:** The company where the domain was registered (e.g., GoDaddy, Namecheap)
- **Registrant Contact:** Person or organization that registered the domain
- **Administrative Contact:** Person responsible for managing the domain
- **Technical Contact:** Person handling technical issues
- **Creation and Expiration Dates:** Registration and expiration timeline
- **Name Servers:** Servers that translate domain names into IP addresses

## Historical Background

WHOIS was created in the 1970s by Elizabeth Feinler and her team at Stanford Research Institute's Network Information Center (NIC). They recognized the need to track growing network resources on ARPANET, the internet's precursor.

## Importance for Web Reconnaissance

WHOIS data provides critical intelligence during penetration testing assessments:

- **Key Personnel Identification:** Names, emails, and phone numbers for social engineering or phishing
- **Network Infrastructure Discovery:** Name servers and IP addresses reveal potential entry points
- **Historical Analysis:** Track ownership and configuration changes over time using services like WhoisFreaks.
