# Other Upload Attacks

In addition to arbitrary file uploads and limited file upload attacks, there are several other techniques and attacks worth mentioning for web penetration tests and bug bounty work.

## Injections in File Name

A common attack uses a malicious string in the uploaded file name, which may get executed if the name is displayed on the page.

**Command Injection Examples:**
- `file$(whoami).jpg`
- `file`whoami`.jpg`
- `file.jpg||whoami`

If the web application uses the file name in an OS command (e.g., `mv file /tmp`), the injected command executes, leading to remote code execution.

**Other Injection Types:**
- **XSS**: `<script>alert(window.origin);</script>`
- **SQL**: `file';select+sleep(5);--.jpg`

## Upload Directory Disclosure

When upload links aren't accessible, several methods can reveal the upload directory:

- **Fuzzing** the uploads directory
- **LFI/XXE vulnerabilities** to read source code
- **Error messages** through forced errors
- Uploading duplicate file names or identical simultaneous requests
- Uploading files with excessively long names (5,000+ characters)

## Windows-Specific Attacks

**Reserved Characters:** `|`, `<`, `>`, `*`, `?` may cause errors and disclose the upload directory.

**Reserved Names:** `CON`, `COM1`, `LPT1`, `NUL` can trigger write errors.

**8.3 Filename Convention:** Use the tilde character (~) to reference or overwrite files.
- `hackthebox.txt` → `HAC~1.TXT` or `HAC~2.TXT`
- Can overwrite sensitive files like `web.conf` via `WEB~1.CON`

Outcomes: information disclosure, DoS, or private file access.

## Advanced File Upload Attacks

Automatic file processing (video encoding, compression, renaming) can be exploited if insecurely coded. Public exploits exist for common libraries (e.g., XXE in ffmpeg). Custom implementations require advanced knowledge to detect vulnerabilities.

Explore bug bounty reports for advanced file upload vulnerability techniques.
