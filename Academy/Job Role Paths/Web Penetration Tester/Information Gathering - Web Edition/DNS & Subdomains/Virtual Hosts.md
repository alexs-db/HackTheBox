# Virtual Hosts

## Overview

Once DNS directs traffic to the correct server, web server configuration determines how incoming requests are handled. Web servers like Apache, Nginx, or IIS host multiple websites or applications on a single server through **virtual hosting**, which differentiates between domains, subdomains, or separate websites with distinct content.

## How Virtual Hosts Work

Web servers distinguish between multiple websites sharing the same IP address using the **HTTP Host header** included in every HTTP request.

### VHosts vs Subdomains

| Aspect | Subdomains | Virtual Hosts (VHosts) |
|--------|-----------|----------------------|
| Definition | Extensions of a main domain (e.g., `blog.example.com`) | Server configurations allowing multiple websites on one server |
| DNS | Have their own DNS records | May not have DNS records |
| Access | Public or internal | Accessible via hosts file modification or DNS |

**VHost fuzzing** discovers public and non-public subdomains by testing various hostnames against a known IP address.

### Example: Apache Configuration

```apacheconf
<VirtualHost *:80>
    ServerName www.example1.com
    DocumentRoot /var/www/example1
</VirtualHost>

<VirtualHost *:80>
    ServerName www.example2.org
    DocumentRoot /var/www/example2
</VirtualHost>
```

## Server VHost Lookup Process

1. **Browser Request**: User enters a domain name (e.g., `www.inlanefreight.com`)
2. **Host Header**: Browser includes domain in the request's Host header
3. **Server Resolution**: Web server examines Host header and consults virtual host configuration
4. **Content Delivery**: Server retrieves corresponding files from the document root

## Types of Virtual Hosting

| Type | Mechanism | Pros | Cons |
|------|-----------|------|------|
| **Name-Based** | HTTP Host header | Cost-effective, no multiple IPs needed, flexible | SSL/TLS limitations |
| **IP-Based** | Unique IP per website | Works with any protocol, better isolation | Expensive, less scalable |
| **Port-Based** | Different ports (80, 8080, etc.) | Works with limited IPs | Less user-friendly |

## Virtual Host Discovery Tools

| Tool | Purpose | Features |
|------|---------|----------|
| **gobuster** | VHost brute-forcing | Fast, custom wordlists, multiple HTTP methods |
| **Feroxbuster** | Directory/VHost fuzzing | Rust-based, recursive, wildcard discovery |
| **ffuf** | Web fuzzing | Quick, customizable, Host header fuzzing |

## Gobuster VHost Discovery

### Prerequisites

- **Target IP**: Identify the web server's IP address
- **Wordlist**: Prepare potential virtual host names (e.g., SecLists)

### Basic Command

```bash
gobuster vhost -u http://<target_IP> -w <wordlist> --append-domain
```

**Flags:**
- `-u`: Target URL
- `-w`: Wordlist file
- `--append-domain`: Append base domain to each word
- `-t`: Number of threads (increase for speed)
- `-k`: Ignore SSL/TLS certificate errors
- `-o`: Save output to file

### Example

```bash
gobuster vhost -u http://inlanefreight.htb:81 -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain
```

**Output:**
```
Found: forum.inlanefreight.htb:81 Status: 200 [Size: 100]
```

## Security Considerations

Virtual host discovery generates significant traffic and may trigger **IDS/WAF** detection. Always obtain proper authorization before scanning targets.
