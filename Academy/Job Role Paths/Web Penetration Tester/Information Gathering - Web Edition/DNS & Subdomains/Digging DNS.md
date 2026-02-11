# Digging DNS

Having established a solid understanding of DNS fundamentals and its various record types, let's now transition to the practical. This section will explore the tools and techniques for leveraging DNS for web reconnaissance.

## DNS Tools

DNS reconnaissance involves utilizing specialized tools designed to query DNS servers and extract valuable information. Here are some of the most popular and versatile tools in the arsenal of web recon professionals:

| Tool | Key Features | Use Cases |
|------|--------------|-----------|
| **dig** | Versatile DNS lookup tool that supports various query types (A, MX, NS, TXT, etc.) and detailed output. | Manual DNS queries, zone transfers (if allowed), troubleshooting DNS issues, and in-depth analysis of DNS records. |
| **nslookup** | Simpler DNS lookup tool, primarily for A, AAAA, and MX records. | Basic DNS queries, quick checks of domain resolution and mail server records. |
| **host** | Streamlined DNS lookup tool with concise output. | Quick checks of A, AAAA, and MX records. |
| **dnsenum** | Automated DNS enumeration tool, dictionary attacks, brute-forcing, zone transfers (if allowed). | Discovering subdomains and gathering DNS information efficiently. |
| **fierce** | DNS reconnaissance and subdomain enumeration tool with recursive search and wildcard detection. | User-friendly interface for DNS reconnaissance, identifying subdomains and potential targets. |
| **dnsrecon** | Combines multiple DNS reconnaissance techniques and supports various output formats. | Comprehensive DNS enumeration, identifying subdomains, and gathering DNS records for further analysis. |
| **theHarvester** | OSINT tool that gathers information from various sources, including DNS records (email addresses). | Collecting email addresses, employee information, and other data associated with a domain from multiple sources. |
| **Online DNS Lookup Services** | User-friendly interfaces for performing DNS lookups. | Quick and easy DNS lookups, convenient when command-line tools are not available, checking for domain availability or basic information. |

## The Domain Information Groper

The `dig` command (Domain Information Groper) is a versatile and powerful utility for querying DNS servers and retrieving various types of DNS records. Its flexibility and detailed customizable output make it a go-to choice.

### Common dig Commands

| Command | Description |
|---------|-------------|
| `dig domain.com` | Performs a default A record lookup for the domain. |
| `dig domain.com A` | Retrieves the IPv4 address (A record) associated with the domain. |
| `dig domain.com AAAA` | Retrieves the IPv6 address (AAAA record) associated with the domain. |
| `dig domain.com MX` | Finds the mail servers (MX records) responsible for the domain. |
| `dig domain.com NS` | Identifies the authoritative name servers for the domain. |
| `dig domain.com TXT` | Retrieves any TXT records associated with the domain. |
| `dig domain.com CNAME` | Retrieves the canonical name (CNAME) record for the domain. |
| `dig domain.com SOA` | Retrieves the start of authority (SOA) record for the domain. |
| `dig @1.1.1.1 domain.com` | Specifies a specific name server to query (e.g., 1.1.1.1). |
| `dig +trace domain.com` | Shows the full path of DNS resolution. |
| `dig -x 192.168.1.1` | Performs a reverse lookup on the IP address 192.168.1.1 to find the associated hostname. |
| `dig +short domain.com` | Provides a short, concise answer to the query. |
| `dig +noall +answer domain.com` | Displays only the answer section of the query output. |
| `dig domain.com ANY` | Retrieves all available DNS records for the domain (Note: Many DNS servers ignore ANY queries per RFC 8482). |

> **⚠️ Caution:** Some servers can detect and block excessive DNS queries. Use caution and respect rate limits. Always obtain permission before performing extensive DNS reconnaissance on a target.

## Digging DNS in Practice

### Example: Basic dig Query

```bash
alexsdb@htb[/htb]$ dig google.com

; <<>> DiG 9.18.24-0ubuntu0.22.04.1-Ubuntu <<>> google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 16449
;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;google.com.                    IN      A

;; ANSWER SECTION:
google.com.             0       IN      A       142.251.47.142

;; Query time: 0 msec
;; SERVER: 172.23.176.1#53(172.23.176.1) (UDP)
;; WHEN: Thu Jun 13 10:45:58 SAST 2024
;; MSG SIZE  rcvd: 54
```

This output is the result of a DNS query using the `dig` command for the domain google.com. It can be broken down into four key sections:

#### Header
- **`opcode: QUERY, status: NOERROR, id: 16449`** — Query type, successful status, and unique identifier.
- **Flags:**
    - `qr` — Query Response flag (indicates this is a response)
    - `rd` — Recursion Desired flag (recursion was requested)
    - `ad` — Authentic Data flag (resolver considers the data authentic)
- **Counts:** 1 question, 1 answer, 0 authority records, 0 additional records.
- **`WARNING: recursion requested but not available`** — Recursion was requested but the server doesn't support it.

#### Question Section
- `google.com. IN A` — Query asking for the IPv4 address (A record) for google.com.

#### Answer Section
- `google.com. 0 IN A 142.251.47.142` — The IP address for google.com is 142.251.47.142. The `0` represents the TTL (time-to-live).

#### Footer
- **Query time** — 0 milliseconds (response time)
- **SERVER** — 172.23.176.1#53 (the DNS server used) and protocol (UDP)
- **WHEN** — Timestamp of the query
- **MSG SIZE** — Size of the DNS response (54 bytes)

> **Note:** An EDNS pseudosection can appear in dig queries, providing support for larger messages and DNSSEC.

### Simplified Output with +short

For a concise answer without additional information, use the `+short` flag:

```bash
alexsdb@htb[/htb]$ dig +short hackthebox.com

104.18.20.126
104.18.21.126
```
