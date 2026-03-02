# Blacklist Filters

## Overview

Web applications often implement file type validation on the back-end to prevent malicious uploads. However, blacklist-based validation is frequently bypassable. This section covers techniques to bypass blacklist filters and upload PHP files.

## Why Blacklists Fail

Blacklist validation compares file extensions against a disallowed list:

```php
$fileName = basename($_FILES["uploadFile"]["name"]);
$extension = pathinfo($fileName, PATHINFO_EXTENSION);
$blacklist = array('php', 'php7', 'phps');

if (in_array($extension, $blacklist)) {
    echo "File type not allowed";
    die();
}
```

**Weaknesses:**
- Incomplete extension lists
- Case-sensitive comparison (Windows is case-insensitive)
- Alternative executable extensions not included (e.g., `.phtml`, `.phar`)

## Bypassing Blacklist Filters

### Method 1: Case Manipulation
Upload with mixed-case extensions: `pHp`, `PhP` (Windows servers only)

### Method 2: Alternative Extensions
Use executable PHP extensions like `.phtml`, `.phar`, `.php7`, `.shtml`

### Method 3: Fuzzing Extensions

1. Intercept upload request in Burp Suite
2. Send to **Intruder** → **Positions** tab
3. Select the extension as the fuzzing point
4. Load extension list (use SecLists or PayloadsAllTheThings)
5. Compare responses:
   - "File successfully uploaded" = allowed extension
   - "Extension not allowed" = blacklisted

### Method 4: Execute Uploaded Shell

Once an allowed extension is found:
1. Upload PHP web shell with new extension (e.g., `.phtml`)
2. Navigate to upload directory (typically `/profile_images/`)
3. Execute shell with command parameters

## Key Takeaway

Always validate files on the back-end with **whitelists**, not blacklists, combined with file content verification.
