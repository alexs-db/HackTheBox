# ZAP Fuzzer

ZAP's Fuzzer is a powerful tool for fuzzing web endpoints. While it lacks some Burp Intruder features, it has a key advantage: it doesn't throttle fuzzing speed, making it faster than Burp's free version.

This section replicates the previous Burp Intruder exercise using ZAP Fuzzer for comparison.

## Setting Up the Fuzz

1. Visit `http://SERVER_IP:PORT/test/` to capture a sample request
2. Right-click the request in proxy history and select **Attack > Fuzz**

The main configuration options are:
- **Fuzz Location** - Where payloads will be inserted
- **Payloads** - The wordlist data to use
- **Processors** - Processing applied to each payload
- **Options** - Attack parameters

## Fuzz Locations

Select the target position (e.g., "test") and click **Add** to mark it with a green indicator.

## Payloads

Click **Add** to select from 8 payload types:
- **File** - Custom wordlist from file
- **File Fuzzers** - Built-in wordlists (dirbuster, etc.)
- **Numberzz** - Number sequences with custom increments

Select **File Fuzzers > dirbuster > directory-list-1.0.txt** and click **Add**.

## Processors

Apply payload processing before injection. Common options:
- Base64 Encode/Decode
- URL Encode/Decode
- MD5/SHA-1/256/512 Hash
- Prefix/Postfix String
- Custom Script

Select **URL Encode** to prevent server errors from special characters. Click **Generate Preview** to verify output.

## Options

Configure attack settings:
- **Concurrent Threads** - Set to 20 for faster scanning
- **Strategy** - Depth First (all words per position) or Breadth First (all positions per word)
- **Retries** - Handle connection errors
- **Follow Redirects** - Optional

## Start Fuzzing

1. Click **Start Fuzzer** to begin
2. Sort results by **Response Code** (200 = success)
3. Click entries to view detailed request/response data

Results show successful hits (e.g., `/skills/` directory with 200 OK response).

Note: Additional fields like **Size Resp. Body** and **RTT** help identify successful hits in different attack scenarios.
