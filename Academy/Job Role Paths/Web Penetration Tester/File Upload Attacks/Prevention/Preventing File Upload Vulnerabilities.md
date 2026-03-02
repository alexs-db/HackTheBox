# Preventing File Upload Vulnerabilities

Throughout this module, we have discussed various methods of exploiting different file upload vulnerabilities. This section outlines action points to rectify identified vulnerabilities during penetration tests or bug bounty exercises.

## Extension Validation

File extensions determine how files and scripts are executed on web servers. Secure extension validation should:

- **Whitelist** allowed extensions (primary defense)
- **Blacklist** dangerous extensions as a secondary layer (e.g., `php`, `phtml`, `phar`)

Example in PHP:

```php
$fileName = basename($_FILES["uploadFile"]["name"]);

// Blacklist dangerous extensions
if (preg_match('/^.*\.ph(p|ps|ar|tml)/', $fileName)) {
    echo "Only images are allowed";
    die();
}

// Whitelist allowed extensions
if (!preg_match('/^.*\.(jpg|jpeg|png|gif)$/', $fileName)) {
    echo "Only images are allowed";
    die();
}
```

Apply validation on both **front-end and back-end** to reduce unintended uploads.

## Content Validation

Validate both file extension and content:

```php
$fileName = basename($_FILES["uploadFile"]["name"]);
$contentType = $_FILES['uploadFile']['type'];
$MIMEtype = mime_content_type($_FILES['uploadFile']['tmp_name']);

// Whitelist extension
if (!preg_match('/^.*\.png$/', $fileName)) {
    echo "Only PNG images are allowed";
    die();
}

// Validate MIME type
foreach (array($contentType, $MIMEtype) as $type) {
    if (!in_array($type, array('image/png'))) {
        echo "Only PNG images are allowed";
        die();
    }
}
```

## Upload Disclosure Prevention

### Hide Upload Directory

- Use a download script (`download.php`) to serve files instead of allowing direct access
- Return **403 Forbidden** for direct directory requests
- Randomize stored file names and store original names in a database

### Security Headers

```
Content-Disposition: attachment
Content-Type: [appropriate MIME type]
X-Content-Type-Options: nosniff
```

### Additional Measures

- Store uploads on a separate server/container
- Use server configurations like `open_basedir` in PHP to restrict file access

## Further Security

- **Disable dangerous functions** in PHP: `exec`, `shell_exec`, `system`, `passthru`
- **Hide error messages** to prevent information disclosure
- **Limit file size**
- **Update libraries** regularly
- **Scan files** for malware
- **Deploy a Web Application Firewall (WAF)** as an additional layer

---

These measures form a comprehensive security checklist for file upload functionality during penetration testing and development.
