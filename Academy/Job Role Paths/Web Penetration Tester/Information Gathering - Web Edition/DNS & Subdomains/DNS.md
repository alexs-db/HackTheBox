# DNS

The Domain Name System (DNS) acts as the internet's GPS, guiding your online journey from memorable landmarks (domain names) to precise numerical coordinates (IP addresses). Much like how GPS translates a destination name into latitude and longitude for navigation, DNS translates human-readable domain names (like www.example.com) into the numerical IP addresses (like 192.0.2.1) that computers use to communicate.

Without DNS, navigating the online world would be akin to driving without a map or GPS – a frustrating and error-prone endeavour.

## How DNS Works

When you enter a domain name into your browser, DNS acts as your navigator, swiftly finding the corresponding IP address and directing your request to the correct destination on the internet.

### DNS Query Process

1. **Your Computer Asks for Directions**: Your computer checks its cache for the IP address. If not found, it reaches out to a DNS resolver, usually provided by your ISP.

2. **The DNS Resolver Checks its Map**: The resolver searches its cache, then queries a root name server if needed.

3. **Root Name Server Points the Way**: The root server directs to the appropriate Top-Level Domain (TLD) name server (e.g., .com, .org).

4. **TLD Name Server Narrows It Down**: The TLD server identifies the authoritative name server for the specific domain.

5. **Authoritative Name Server Delivers the Address**: This server holds the correct IP address and returns it to the resolver.

6. **The DNS Resolver Returns the Information**: The resolver caches and returns the IP address to your computer.

7. **Your Computer Connects**: Your computer can now connect directly to the web server.

## The Hosts File

The hosts file is a simple text file used to map hostnames to IP addresses, providing a manual method of domain name resolution that bypasses DNS.

**Location:**
- Windows: `C:\Windows\System32\drivers\etc\hosts`
- Linux/MacOS: `/etc/hosts`

**Format:**
```
<IP Address>    <Hostname> [<Alias> ...]
```

**Examples:**
```
127.0.0.1       localhost
192.168.1.10    devserver.local
127.0.0.1       myapp.local
0.0.0.0         unwanted-site.com
```

## Key DNS Concepts

### DNS Zones

A DNS zone is a distinct part of the domain namespace managed by a specific entity. The zone file defines resource records within this zone.

**Example zone file for example.com:**
```zone
$TTL 3600
@       IN SOA   ns1.example.com. admin.example.com. (
                2024060401 ; Serial
                3600       ; Refresh
                900        ; Retry
                604800     ; Expire
                86400 )    ; Minimum TTL

@       IN NS    ns1.example.com.
@       IN NS    ns2.example.com.
@       IN MX 10 mail.example.com.
www     IN A     192.0.2.1
mail    IN A     198.51.100.1
ftp     IN CNAME www.example.com.
```

### Core Concepts

| Term | Description | Example |
|------|-------------|---------|
| Domain Name | Human-readable label | www.example.com |
| IP Address | Unique numerical identifier | 192.0.2.1 |
| DNS Resolver | Translates domain names to IP addresses | 8.8.8.8 (Google DNS) |
| Root Name Server | Top-level DNS hierarchy | a.root-servers.net |
| TLD Name Server | Manages .com, .org, etc. | Verisign for .com |
| Authoritative Name Server | Holds actual IP addresses | Hosting provider servers |

## DNS Record Types

| Type | Full Name | Description | Example |
|------|-----------|-------------|---------|
| A | Address Record | Maps hostname to IPv4 | `www.example.com. IN A 192.0.2.1` |
| AAAA | IPv6 Address Record | Maps hostname to IPv6 | `www.example.com. IN AAAA 2001:db8::1` |
| CNAME | Canonical Name | Creates hostname alias | `blog.example.com. IN CNAME www.example.com.` |
| MX | Mail Exchange | Specifies mail server | `example.com. IN MX 10 mail.example.com.` |
| NS | Name Server | Delegates DNS zone | `example.com. IN NS ns1.example.com.` |
| TXT | Text Record | Stores text info (SPF, DKIM) | `example.com. IN TXT "v=spf1 mx -all"` |
| SOA | Start of Authority | Zone administrative info | `example.com. IN SOA ns1.example.com. admin.example.com. ...` |
| SRV | Service Record | Service location & port | `_sip._udp.example.com. IN SRV 10 5 5060 sipserver.example.com.` |
| PTR | Pointer Record | Reverse DNS lookup | `1.2.0.192.in-addr.arpa. IN PTR www.example.com.` |

**Note:** The "IN" field indicates Internet protocol class, standard for all modern DNS records.

## Why DNS Matters for Web Recon

DNS is critical for penetration testing and reconnaissance:

- **Uncovering Assets**: DNS records reveal subdomains, mail servers, and name servers that may be outdated or vulnerable.
- **Mapping Network Infrastructure**: Analyse DNS data to create comprehensive maps of target infrastructure, identify hosting providers via NS records, and pinpoint potential weaknesses.
- **Monitoring for Changes**: Track DNS record changes over time to detect new entry points (new subdomains) or technology use (e.g., `_1password=...` TXT records) that could be leveraged for social engineering or phishing campaigns.
