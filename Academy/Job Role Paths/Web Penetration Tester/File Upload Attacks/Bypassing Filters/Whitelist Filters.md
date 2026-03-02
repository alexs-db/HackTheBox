# Whitelist Filters

Whitelist validation is generally more secure than blacklist validation. The web server only allows specified extensions, reducing the need for comprehensive coverage of uncommon extensions.

Both blacklist and whitelist approaches have use cases:
- **Blacklist**: Helpful when upload functionality must allow many file types (e.g., File Manager)
- **Whitelist**: Used when only a few file types are allowed
- Both can be used together

## Whitelisting Extensions

When uploading uncommon PHP extensions like `.phtml`, you may encounter "Only images are allowed" messages. This doesn't reveal the validation method used.

### Vulnerable Regex Pattern

A common vulnerability exists in weak regex patterns:

```php
$fileName = basename($_FILES["uploadFile"]["name"]);

if (!preg_match('^.*\.(jpg|jpeg|png|gif)', $fileName)) {
    echo "Only images are allowed";
    die();
}
```

This regex only checks if the filename *contains* an image extension, not if it *ends* with one.

## Bypass Techniques

### Double Extensions

Since the regex only checks for extension presence, you can add `.jpg` to a PHP filename:

```
shell.jpg.php
```

This passes the whitelist test while remaining executable as PHP.

### Strict Regex Pattern

A proper regex pattern uses anchors:

```php
if (!preg_match('/^.*\.(jpg|jpeg|png|gif)$/', $fileName)) { ... }
```

This only matches files *ending* with allowed extensions.

### Reverse Double Extension

Web server misconfigurations can bypass strict patterns. For example, Apache's PHP handler:

```xml
<FilesMatch ".+\.ph(ar|p|tml)">
    SetHandler application/x-httpd-php
</FilesMatch>
```

A file named `shell.php.jpg` passes the whitelist (ends with `.jpg`) but executes PHP (contains `.php`).

### Character Injection

Inject special characters before or after the extension to bypass validation:

| Character | Use Case |
|-----------|----------|
| `%20` (space) | Various servers |
| `%0a`, `%0d0a` | Newline tricks |
| `%00` | PHP ≤5.X null byte |
| `:` | Windows servers (e.g., `shell.aspx:.jpg`) |
| `/`, `.\` | Path traversal tricks |

**Example bash script** for generating permutations:

```bash
for char in '%20' '%0a' '%00' '%0d0a' '/' '.\\' '.' '…' ':'; do
    for ext in '.php' '.phps'; do
        echo "shell$char$ext.jpg" >> wordlist.txt
        echo "shell$ext$char.jpg" >> wordlist.txt
        echo "shell.jpg$char$ext" >> wordlist.txt
        echo "shell.jpg$ext$char" >> wordlist.txt
    done
done
```

Use this wordlist with Burp Intruder to test for vulnerabilities in outdated or misconfigured systems.
