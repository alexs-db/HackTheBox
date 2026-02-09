# Burp Intruder

Both Burp and ZAP provide features beyond the default web proxy, including web fuzzers and web scanners. Built‑in fuzzers can handle fuzzing, enumeration, and brute‑forcing, and often replace CLI tools like ffuf, dirbuster, gobuster, and wfuzz.

**Burp Intruder** is Burp’s web fuzzer. It can fuzz pages, directories, sub‑domains, parameters, and values. The Community edition is throttled to **1 request/second**, so it’s suitable only for short scans. Burp Pro removes this limit and adds advanced features.

---

## Target

1. Open Burp and the pre‑configured browser.
2. Visit the target application.
3. In **Proxy > HTTP history**, right‑click the request and choose **Send to Intruder** (Ctrl+I).
4. Open **Intruder** (Ctrl+Shift+I).

The **Target** section shows the host/port from the captured request.

---

## Positions

Positions define where payloads are inserted.

To fuzz directories, use:

```
GET /DIRECTORY/
```

Select `DIRECTORY` and click **Add §** to mark it as the payload position.

> **Note:** Keep the two empty lines at the end of the request to avoid server errors.

---

## Payloads

Configure payloads on the right panel. There are four areas:

1. **Payload Position & Type**
2. **Payload Configuration**
3. **Payload Processing**
4. **Payload Encoding**

### Payload Position & Type

Select **Payload Set 1 - DIRECTORY** (Sniper attack uses a single position).  
Use **Simple list** as the payload type.

Other types include:
- **Runtime file**: loads items line‑by‑line to save memory.
- **Character substitution**: generates permutations.

### Payload Configuration

Load a wordlist:

```
/opt/useful/seclists/Discovery/Web-Content/common.txt
```

You can add multiple lists or manual entries.  
In Burp Pro, you can use **Add from list** to choose built‑in lists.

> **Tip:** Use **Runtime file** for large lists.

### Payload Processing

Example: skip lines starting with `.`  
Add rule **Skip if matches regex** with:

```
^\..*$
```

### Payload Encoding

Leave **URL‑encode** enabled.

---

## Settings

Adjust options in **Settings**:

- Set **Number of retries** and **Pause before retry** to `0`.
- Enable **Grep - Match**, clear existing rules, then add:

```
200 OK
```

Disable **Exclude HTTP headers** so the header is searched.

**Grep - Extract** is optional; not needed for this case.

---

## Attack

Click **Start attack**. In Community edition, scans are slow.

You should see skipped lines (starting with `.`), then results.  
Sort by **200 OK**, **Status**, or **Length**.  
Example hit:

```
/admin/
```

Verify:

```
http://SERVER_IP:PORT/admin/
```

---

## Notes

Burp Intruder can also:

- brute‑force passwords
- fuzz parameters
- perform password spraying (e.g., OWA, VPN portals, RDS, Citrix, custom AD apps)

Because Community edition is throttled, the next section uses **ZAP Fuzzer** for faster scans.
