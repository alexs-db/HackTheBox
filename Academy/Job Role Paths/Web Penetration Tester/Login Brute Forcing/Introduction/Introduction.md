# Introduction

Keys and passwords are the modern equivalent of locks and combinations.  
Brute forcing is the process of trying many possible combinations until one works.

## What Is Brute Forcing?

In cybersecurity, **brute forcing** is a trial-and-error technique used to crack:

- passwords
- login credentials
- encryption keys

An attacker systematically tests combinations until the correct one is found.

The success of a brute-force attack depends mainly on:

1. **Password/key complexity**  
    Longer values with mixed character types (uppercase, lowercase, numbers, symbols) are much harder to crack.
2. **Available computing power**  
    Faster hardware can test far more combinations per second.
3. **Defensive controls**  
    Lockout policies, CAPTCHAs, rate limits, and monitoring can slow or block attempts.

## How Brute Forcing Works

Typical process:

1. **Start**  
    The attacker launches brute-force tooling.
2. **Generate combination**  
    The tool creates a candidate based on defined rules (charset, length, patterns).
3. **Apply combination**  
    The candidate is tested against a target (e.g., login form, encrypted file).
4. **Check result**  
    If correct, access is obtained; otherwise, testing continues.
5. **Repeat / End**  
    The cycle repeats until success or termination.

## Types of Brute Forcing

| Method | Description | Example | Best Used When... |
|---|---|---|---|
| **Simple Brute Force** | Tries all combinations within a charset and length range. | Testing all lowercase passwords of length 4–6. | No prior password insight; compute resources are strong. |
| **Dictionary Attack** | Uses common word/password lists. | Trying entries from `rockyou.txt`. | Users likely choose weak/common passwords. |
| **Hybrid Attack** | Dictionary + mutations (suffixes/prefixes/symbols). | Appending `123!` to dictionary words. | Passwords are likely slightly modified common words. |
| **Credential Stuffing** | Reuses leaked username/password pairs across services. | Testing breach credentials on other platforms. | Reused passwords are likely. |
| **Password Spraying** | Tries a few common passwords across many accounts. | Trying `Password123!` against all users. | Lockout controls exist; attacker wants low-and-slow attempts. |
| **Rainbow Table Attack** | Uses precomputed hash tables to reverse hashes quickly. | Matching captured hashes against prebuilt tables. | Many hashes must be cracked and storage is available. |
| **Reverse Brute Force** | Tests one known password against many usernames. | Trying one leaked password across multiple accounts. | A reused password is strongly suspected. |
| **Distributed Brute Force** | Splits attempts across many systems/devices. | Using a compute cluster to increase throughput. | Target secrets are complex and single-host cracking is too slow. |

## The Role of Brute Forcing in Penetration Testing

In ethical hacking, brute forcing is used to evaluate the strength of password-based authentication.

It is commonly considered when:

- **Other attack paths fail** (e.g., known exploit paths are exhausted).
- **Password policy is weak** (short/simple or predictable passwords).
- **Specific accounts matter** (e.g., privileged or high-value targets).

Used responsibly, it helps identify weaknesses so organizations can improve defenses before real attackers exploit them.
