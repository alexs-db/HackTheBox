# Hybrid Attacks

Many organizations implement policies requiring periodic password changes. However, these policies can breed predictable password patterns if users lack proper password hygiene education.

A common insecure practice is making minor modifications when password changes are mandatory. Users often append numbers or special characters to existing passwords (e.g., "Summer2023" → "Summer2023!" or "Summer2024"). This predictable behavior enables hybrid attacks, which combine dictionary and brute-force techniques to exploit password patterns.

## Hybrid Attacks in Action

Consider an attacker targeting an organization enforcing regular password changes:

1. **Dictionary Attack Phase**: Uses a wordlist of common passwords, industry terms, and organization-specific information to identify weak passwords
2. **Brute-Force Transition**: If unsuccessful, strategically modifies dictionary words by appending numbers, special characters, or incrementing years
3. **Result**: Drastically reduces search space while covering likely password variations

## Filtering Passwords by Policy

Given a password policy requiring:
- Minimum 8 characters
- At least one uppercase letter
- At least one lowercase letter
- At least one number

Use grep with regex to filter a wordlist:

```bash
# Download wordlist
wget https://raw.githubusercontent.com/danielmiessler/SecLists/refs/heads/master/Passwords/Common-Credentials/darkweb2017_top-10000.txt

# Filter by minimum length
grep -E '^.{8,}$' darkweb2017-top10000.txt > darkweb2017-minlength.txt

# Filter uppercase
grep -E '[A-Z]' darkweb2017-minlength.txt > darkweb2017-uppercase.txt

# Filter lowercase
grep -E '[a-z]' darkweb2017-uppercase.txt > darkweb2017-lowercase.txt

# Filter numbers
grep -E '[0-9]' darkweb2017-lowercase.txt > darkweb2017-number.txt

# Count results
wc -l darkweb2017-number.txt
# Output: 89 darkweb2017-number.txt
```

This filtering reduces 10,000 passwords to 89, significantly optimizing attack efficiency.

## Credential Stuffing

Credential stuffing exploits password reuse across multiple accounts. Attackers acquire compromised credentials from data breaches or phishing, then systematically test them against target services using automated tools.

**Success factors:**
- Users reuse passwords across platforms
- Attackers target high-value services (email, banking, social media)
- Automated testing mimics normal user behavior

**Mitigation**: Use unique, strong passwords for each account and enable multi-factor authentication.
