# Custom Wordlists

## Overview

While pre-made wordlists like rockyou or SecLists provide extensive repositories of potential passwords and usernames, they operate on a broad spectrum. This approach can be inefficient when targeting specific individuals or organizations with unique patterns.

**Example:** A generic username list is unlikely to match "Thomas Edison" at his workplace, where specific username conventions (e.g., firstname/lastname or lastname/first3chars) are enforced.

Custom wordlists—tailored to the specific target and their environment—dramatically increase brute-force efficiency and success rates by leveraging:
- Social media profiles
- Company directories
- Leaked data

## Username Anarchy

Manual username generation for even simple names becomes complex. Beyond obvious combinations (jane, smith, janesmith, j.smith), targets often use:
- Middle names and birth years: janemarie, smithj87
- Leetspeak: j4n3, 5m1th, j@n3_5m1th
- Personal interests: winteriscoming, potterheadjane

**Username Anarchy** generates these variations automatically:

```bash
sudo apt install ruby -y
git clone https://github.com/urbanadventurer/username-anarchy.git
cd username-anarchy
./username-anarchy Jane Smith > jane_smith_usernames.txt
```

This produces combinations including: janesmith, jane.smith, js, j.s., and more.

## CUPP (Common User Passwords Profiler)

CUPP creates personalized password wordlists using gathered intelligence. Effectiveness depends on information quality gathered from:
- **Social Media:** Birthdays, pet names, favorite quotes, interests
- **Company Websites:** Position, professional bio
- **Public Records:** Address, family members, property ownership
- **News/Blogs:** Achievements, affiliations

### Example Profile

| Field | Details |
|-------|---------|
| Name | Jane Smith |
| Nickname | Janey |
| Birthdate | 11/12/1990 |
| Partner | Jim (Jimbo) - 12/12/1990 |
| Pet | Spot |
| Company | AHI |
| Interests | Hackers, Pizza, Golf, Horses |
| Colors | Blue |

### Installation & Usage

```bash
sudo apt install cupp -y
cupp -i
```

Follow the interactive prompts, then CUPP generates variations including:
- Original/capitalized: jane, Jane
- Reversed: enaj, enaJ
- Dates: jane1990, smith1211
- Concatenations: janesmith, smithjane
- Special chars & numbers: jane!, smith123
- Leetspeak: j4n3, 5m1th

Result: ~46,790 potential passwords in jane.txt

## Password Policy Filtering

If the target enforces specific requirements (e.g., 6+ chars, 1 uppercase, 1 lowercase, 1 number, 2 special chars):

```bash
grep -E '^.{6,}$' jane.txt | grep -E '[A-Z]' | grep -E '[a-z]' | \
grep -E '[0-9]' | grep -E '([!@#$%^&*].*){2,}' > jane-filtered.txt
```

This reduces ~46,000 passwords to ~7,900 matching candidates.

## Brute-Force Attack with Hydra

```bash
hydra -L jane_smith_usernames.txt -P jane-filtered.txt IP -s PORT -f \
http-post-form "/:username=^USER^&password=^PASS^:Invalid credentials"
```

Once credentials are discovered, log in and retrieve the flag.
