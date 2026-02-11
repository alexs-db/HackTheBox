# Introduction

Web Reconnaissance is the foundation of a thorough security assessment. It involves systematically collecting information about a target website or web application—essentially the preparatory phase before deeper analysis and potential exploitation. This forms a critical part of the "Information Gathering" phase of the Penetration Testing Process.

## Primary Goals

- **Identifying Assets**: Uncovering publicly accessible components (web pages, subdomains, IP addresses, technologies)
- **Discovering Hidden Information**: Locating inadvertently exposed sensitive data (backup files, configuration files, documentation)
- **Analysing the Attack Surface**: Examining vulnerabilities, weaknesses, and potential exploitation entry points
- **Gathering Intelligence**: Collecting information for exploitation or social engineering (key personnel, email patterns, etc.)

Attackers use this information to tailor and target specific weaknesses, while defenders use recon to proactively identify and patch vulnerabilities.

## Types of Reconnaissance

Web reconnaissance uses two methodologies: **active** and **passive** reconnaissance.

### Active Reconnaissance

Direct interaction with the target system to gather information.

| Technique | Description | Risk |
|-----------|-------------|------|
| Port Scanning | Identifying open ports and services | High |
| Vulnerability Scanning | Probing for known vulnerabilities | High |
| Network Mapping | Mapping network topology | Medium-High |
| Banner Grabbing | Retrieving service information | Low |
| OS Fingerprinting | Identifying the operating system | Low |
| Service Enumeration | Determining service versions | Low |
| Web Spidering | Crawling to discover resources | Low-Medium |

**Advantage**: Comprehensive view of infrastructure. **Disadvantage**: Higher detection risk.

### Passive Reconnaissance

Gathering information without direct target interaction, using publicly available resources.

| Technique | Risk |
|-----------|------|
| Search Engine Queries | Very Low |
| WHOIS Lookups | Very Low |
| DNS Analysis | Very Low |
| Web Archive Analysis | Very Low |
| Social Media Analysis | Very Low |
| Code Repositories | Very Low |

**Advantage**: Stealthier approach. **Disadvantage**: Less comprehensive information.

## Next Steps

This module covers essential tools and techniques for web reconnaissance, starting with WHOIS—a gateway to accessing vital domain registration and ownership information.
