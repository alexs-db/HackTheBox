# Subdomain Bruteforcing

## Overview

Subdomain Brute-Force Enumeration is a powerful active subdomain discovery technique that leverages pre-defined lists of potential subdomain names. This approach systematically tests these names against the target domain to identify valid subdomains.

## Process

The brute-forcing process consists of four main steps:

1. **Wordlist Selection**: Choose a wordlist containing potential subdomain names
    - General-Purpose: Common subdomain names (dev, staging, blog, mail, admin, test)
    - Targeted: Industry or technology-specific patterns
    - Custom: Based on gathered intelligence

2. **Iteration and Querying**: A tool iterates through the wordlist, appending each word to the main domain (e.g., `dev.example.com`)

3. **DNS Lookup**: Perform DNS queries for each potential subdomain using A or AAAA record types

4. **Filtering and Validation**: Confirm successful resolutions and validate subdomain functionality

## Tools

| Tool | Description |
|------|-------------|
| dnsenum | Comprehensive DNS enumeration with dictionary and brute-force attacks |
| fierce | Recursive subdomain discovery with wildcard detection |
| dnsrecon | Versatile DNS reconnaissance with customizable output |
| amass | Actively maintained with extensive data sources |
| assetfinder | Simple, lightweight subdomain finder |
| puredns | Powerful DNS brute-forcing and filtering tool |

## DNSenum

**dnsenum** is a Perl-based DNS reconnaissance tool offering:
- DNS Record Enumeration (A, AAAA, NS, MX, TXT)
- Zone Transfer Attempts
- Subdomain Brute-Forcing
- Google Scraping
- Reverse DNS Lookups
- WHOIS Queries

### Example Usage

```bash
dnsenum --enum inlanefreight.com -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -r
```

**Command breakdown:**
- `--enum`: Enable enumeration with tuning options
- `-f`: Specify wordlist path
- `-r`: Enable recursive subdomain brute-forcing

### Sample Output

```
dnsenum VERSION:1.2.6

-----   inlanefreight.com   -----

Host's addresses:
inlanefreight.com.                       300      IN    A        134.209.24.248

Brute forcing with /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt:

www.inlanefreight.com.                   300      IN    A        134.209.24.248
support.inlanefreight.com.               300      IN    A        134.209.24.248
```
