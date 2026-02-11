# DNS Zone Transfers

## Overview

DNS zone transfers, while designed for legitimate DNS server replication, can become a significant security vulnerability if misconfigured. This technique allows attackers to obtain a complete list of subdomains, IP addresses, and other sensitive DNS information.

## What is a Zone Transfer?

A DNS zone transfer is a complete copy of all DNS records within a zone from one name server to another. It's essential for DNS redundancy but poses a security risk when improperly secured.

### Zone Transfer Process

1. **Zone Transfer Request (AXFR)**: The secondary DNS server sends an AXFR request to the primary server
2. **SOA Record Transfer**: The primary server responds with its Start of Authority (SOA) record
3. **DNS Records Transmission**: All DNS records (A, AAAA, MX, CNAME, NS, etc.) are transferred
4. **Zone Transfer Complete**: The primary server signals transfer completion
5. **Acknowledgement (ACK)**: The secondary server confirms successful receipt

## The Vulnerability

Misconfigured DNS servers may allow unauthorized zone transfers, exposing:

- **Subdomains**: Development servers, staging environments, admin panels
- **IP Addresses**: Potential targets for further attacks
- **Name Server Records**: DNS infrastructure details and provider information

## Remediation

Modern DNS servers are typically configured to restrict zone transfers to trusted secondary servers. However, misconfigurations still occur due to human error or outdated practices.

## Exploiting Zone Transfers

Use `dig` to attempt a zone transfer:

```bash
dig axfr @nsztm1.digi.ninja zonetransfer.me
```

### Example Output

```
zonetransfer.me.    7200    IN  SOA     nsztm1.digi.ninja. robin.digi.ninja. 2019100801 172800 900 1209600 3600
zonetransfer.me.    300     IN  HINFO   "Casio fx-700G" "Windows XP"
zonetransfer.me.    7200    IN  MX      0 ASPMX.L.GOOGLE.COM.
zonetransfer.me.    7200    IN  A       5.196.105.14
zonetransfer.me.    7200    IN  NS      nsztm1.digi.ninja.
asfdbbox.zonetransfer.me.    7200    IN  A   127.0.0.1
canberra-office.zonetransfer.me.    7200    IN  A   202.14.81.230

;; XFR size: 50 records (messages 1, bytes 2085)
```

**Note**: `zonetransfer.me` is a deliberately vulnerable domain for educational purposes.
