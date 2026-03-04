# Medusa

Medusa is a fast, massively parallel, and modular login brute-forcer designed for penetration testing. It supports a wide array of services that allow remote authentication, enabling security professionals to assess login system resilience.

## Installation

Medusa often comes pre-installed on penetration testing distributions. Verify installation:

```bash
medusa -h
```

On Linux systems:

```bash
sudo apt-get -y update
sudo apt-get -y install medusa
```

## Command Syntax

```bash
medusa [target_options] [credential_options] -M module [module_options]
```

### Common Parameters

| Parameter | Explanation | Example |
|-----------|-------------|---------|
| `-h HOST` / `-H FILE` | Target host or file list | `medusa -h 192.168.1.10` |
| `-u USERNAME` / `-U FILE` | Username or file list | `medusa -U usernames.txt` |
| `-p PASSWORD` / `-P FILE` | Password or file list | `medusa -P passwords.txt` |
| `-M MODULE` | Module (ssh, ftp, http, etc.) | `medusa -M ssh` |
| `-m "OPTION"` | Module-specific options | `medusa -M http -m "POST /login.php"` |
| `-t TASKS` | Parallel login attempts | `medusa -t 4` |
| `-f` / `-F` | Stop after first success | `medusa -f` |
| `-n PORT` | Non-default port | `medusa -n 2222` |
| `-v LEVEL` | Verbose output (0-6) | `medusa -v 4` |

## Supported Modules

| Module | Service | Example |
|--------|---------|---------|
| ftp | FTP | `medusa -M ftp -h 192.168.1.100 -u admin -P passwords.txt` |
| http | HTTP Forms | `medusa -M http -h www.example.com -U users.txt -P passwords.txt` |
| imap | Email (IMAP) | `medusa -M imap -h mail.example.com -U users.txt -P passwords.txt` |
| mysql | MySQL Database | `medusa -M mysql -h 192.168.1.100 -u root -P passwords.txt` |
| pop3 | Email (POP3) | `medusa -M pop3 -h mail.example.com -U users.txt -P passwords.txt` |
| rdp | Remote Desktop | `medusa -M rdp -h 192.168.1.100 -u admin -P passwords.txt` |
| ssh | SSH | `medusa -M ssh -h 192.168.1.100 -u root -P passwords.txt` |
| svn | Subversion | `medusa -M svn -h 192.168.1.100 -u admin -P passwords.txt` |
| telnet | Telnet | `medusa -M telnet -h 192.168.1.100 -u admin -P passwords.txt` |
| vnc | VNC | `medusa -M vnc -h 192.168.1.100 -P passwords.txt` |

## Usage Examples

### SSH Brute-Force Attack

```bash
medusa -h 192.168.0.100 -U usernames.txt -P passwords.txt -M ssh
```

### Multiple Web Servers with HTTP Authentication

```bash
medusa -H web_servers.txt -U usernames.txt -P passwords.txt -M http -m GET
```

### Test for Empty or Default Passwords

```bash
medusa -h 10.0.0.5 -U usernames.txt -e ns -M ssh
```

This tests for empty passwords (`-e n`) and passwords matching usernames (`-e s`).
