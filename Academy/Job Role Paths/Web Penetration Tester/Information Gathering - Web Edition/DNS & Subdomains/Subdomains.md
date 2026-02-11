# Subdomains

When exploring DNS records, we've primarily focused on the main domain (e.g., example.com). However, subdomains—extensions of the main domain—often organize different sections or functionalities. For example: blog.example.com, shop.example.com, or mail.example.com.

## Why Subdomains Matter for Reconnaissance

Subdomains often host valuable information not directly linked from the main website:

- **Development and Staging Environments**: Test environments with relaxed security may expose vulnerabilities or sensitive information
- **Hidden Login Portals**: Administrative panels or login pages not meant to be public
- **Legacy Applications**: Outdated software with known vulnerabilities
- **Sensitive Information**: Confidential documents, internal data, or configuration files

## Subdomain Enumeration

Subdomain enumeration systematically identifies these subdomains. From a DNS perspective, subdomains use A (or AAAA for IPv6) records mapping subdomain names to IP addresses, and CNAME records for aliases.

### Active Enumeration

Directly queries the target's DNS servers:
- **DNS Zone Transfer**: Exploits misconfigured servers (rarely successful now)
- **Brute-Force**: Tests potential subdomain names using tools like dnsenum, ffuf, or gobuster with common wordlists

### Passive Enumeration

Uses external sources without directly querying the target:
- **Certificate Transparency Logs**: SSL/TLS certificates list subdomains in the Subject Alternative Name (SAN) field
- **Search Engines**: Uses operators like `site:` to filter results
- **Online Databases**: Aggregates DNS data from multiple sources

## Combined Approach

Active enumeration offers more control but is more detectable. Passive enumeration is stealthier but may miss subdomains. Combining both methods provides the most thorough strategy.
