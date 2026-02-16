# Decoding

After completing the previous exercise, we obtained encoded text that needs to be decoded:

```bash
alexsdb@htb[/htb]$ curl http://SERVER_IP:PORT/serial.php -X POST -d "param1=sample"
ZG8gdGhlIGV4ZXJjaXNlLCBkb24ndCBjb3B5IGFuZCBwYXN0ZSA7KQo=
```

Obfuscated code typically contains encoded text blocks that are decoded during execution. This section covers three common encoding methods:

- **Base64**
- **Hex**
- **ROT13**

## Base64

Base64 encoding reduces special characters by representing data as alpha-numeric characters plus `+` and `/`.

### Identifying Base64

Base64 strings use alpha-numeric characters and are padded with `=` to reach a multiple of 4 characters.

### Encoding

```bash
alexsdb@htb[/htb]$ echo https://www.hackthebox.eu/ | base64
aHR0cHM6Ly93d3cuaGFja3RoZWJveC5ldS8K
```

### Decoding

```bash
alexsdb@htb[/htb]$ echo aHR0cHM6Ly93d3cuaGFja3RoZWJveC5ldS8K | base64 -d
https://www.hackthebox.eu/
```

## Hex

Hex encoding converts each character to its ASCII hexadecimal value (a=61, b=62, etc.).

### Identifying Hex

Hex strings contain only hex characters: `0-9` and `a-f`.

### Encoding

```bash
alexsdb@htb[/htb]$ echo https://www.hackthebox.eu/ | xxd -p
68747470733a2f2f7777772e6861636b746865626f782e65752f0a
```

### Decoding

```bash
alexsdb@htb[/htb]$ echo 68747470733a2f2f7777772e6861636b746865626f782e65752f0a | xxd -p -r
https://www.hackthebox.eu/
```

## ROT13

ROT13 is a Caesar cipher that shifts each letter 13 positions forward.

### Identifying ROT13

ROT13 text appears random but maintains structural patterns (e.g., `http://www` becomes `uggc://jjj`).

### Encoding/Decoding

```bash
alexsdb@htb[/htb]$ echo https://www.hackthebox.eu/ | tr 'A-Za-z' 'N-ZA-Mn-za-m'
uggcf://jjj.unpxgurobk.rh/
```

## Other Encoding Methods

Hundreds of encoding methods exist. When encountering unknown encodings:

1. Attempt to identify the type
2. Search for online decoding tools
3. Use automated tools like [Cipher Identifier](https://www.dcode.fr/cipher-identifier)

**Note:** Beyond encoding, obfuscation often uses encryption (encoding with a key), making reverse engineering significantly more difficult.
