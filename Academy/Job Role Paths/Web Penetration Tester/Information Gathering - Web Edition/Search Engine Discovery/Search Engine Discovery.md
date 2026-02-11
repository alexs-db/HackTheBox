# Search Engine Discovery

Search engines are powerful tools for web reconnaissance and information gathering through **OSINT (Open Source Intelligence)**. They help uncover publicly accessible data about target websites, organizations, and individuals—from employee information to exposed credentials.

## Why It Matters

- **Open Source**: Legally and ethically gathered public information
- **Breadth**: Indexes vast portions of the web
- **Accessible**: User-friendly, no specialized skills required
- **Cost-effective**: Free resource

### Applications

- Security Assessment: Identifying vulnerabilities and attack vectors
- Competitive Intelligence: Analyzing competitors' strategies
- Investigative Journalism: Uncovering hidden connections
- Threat Intelligence: Tracking threats and malicious actors

**Note**: Search engines don't index all information; some data is intentionally hidden or protected.

## Search Operators

Search operators enable precise queries to find specific information types.

| Operator | Purpose | Example |
|----------|---------|---------|
| `site:` | Limit to specific domain | `site:example.com` |
| `inurl:` | Term in URL | `inurl:login` |
| `filetype:` | Specific file type | `filetype:pdf` |
| `intitle:` | Term in page title | `intitle:"confidential report"` |
| `intext:` | Term in body text | `intext:"password reset"` |
| `cache:` | Cached page version | `cache:example.com` |
| `link:` | Pages linking to target | `link:example.com` |
| `related:` | Similar websites | `related:example.com` |
| `"..."` | Exact phrase | `"information security policy"` |
| `OR` | Include any term | `"linux" OR "ubuntu"` |
| `NOT` | Exclude term | `site:bank.com NOT inurl:login` |
| `*` | Wildcard | `site:example.com user* manual` |

## Google Dorking

Google Dorking leverages search operators to uncover sensitive data and vulnerabilities.

**Login Pages:**
```
site:example.com inurl:login
site:example.com (inurl:login OR inurl:admin)
```

**Exposed Files:**
```
site:example.com filetype:pdf
site:example.com (filetype:xls OR filetype:docx)
```

**Configuration Files:**
```
site:example.com inurl:config.php
site:example.com (ext:conf OR ext:cnf)
```

**Database Backups:**
```
site:example.com inurl:backup
site:example.com filetype:sql
```

For more examples, refer to the [Google Hacking Database](https://www.exploit-db.com/google-hacking-database).
