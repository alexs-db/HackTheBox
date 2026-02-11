# Certificate Transparency Logs

## Overview

Certificate Transparency (CT) logs are public, append-only ledgers that record the issuance of SSL/TLS certificates. Whenever a Certificate Authority (CA) issues a new certificate, it must submit it to multiple CT logs maintained by independent organizations.

### Key Benefits

- **Early Detection of Rogue Certificates**: Identify suspicious or misissued certificates quickly
- **Accountability for CAs**: Public visibility of issuance practices
- **Strengthening Web PKI**: Enhanced security through public verification

## CT Logs in Web Reconnaissance

CT logs provide a definitive record of certificates issued for a domain and its subdomains, offering advantages over brute-forcing or wordlist-based approaches. They reveal:

- Subdomains with issued certificates
- Historical records of inactive or expired certificates
- Potentially vulnerable legacy systems

## Tools for Searching CT Logs

| Tool | Features | Pros | Cons |
|------|----------|------|------|
| **crt.sh** | Web interface, domain search, certificate details | Free, no registration | Limited filtering |
| **Censys** | Advanced filtering, API access, device intelligence | Powerful analysis | Requires registration |

## Example: crt.sh API Lookup

Find all 'dev' subdomains on facebook.com:

```bash
curl -s "https://crt.sh/?q=facebook.com&output=json" | jq -r '.[] | select(.name_value | contains("dev")) | .name_value' | sort -u
```

**Output:**
```
*.dev.facebook.com
*.newdev.facebook.com
dev.facebook.com
newdev.facebook.com
```

### Command Breakdown

- `curl`: Fetches JSON output from crt.sh
- `jq`: Filters results for entries containing "dev"
- `sort -u`: Sorts and removes duplicates
