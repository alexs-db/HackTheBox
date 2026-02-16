# Introduction to XSS

## Introduction

As web applications become more advanced and prevalent, so do web application vulnerabilities. Cross-Site Scripting (XSS) is among the most common types of web application vulnerabilities, exploiting flaws in user input sanitization to inject and execute JavaScript code on the client side.

## What is XSS?

A typical web application receives HTML from the back-end server and renders it in the client-side browser. When a vulnerable application fails to sanitize user input properly, malicious users can inject JavaScript code into input fields (comments, replies, etc.). When other users view the page, they unknowingly execute the malicious code.

**Key characteristics:**
- Executed solely on the client-side
- Does not directly affect the back-end server
- Only impacts the executing user
- High probability + low direct impact = medium risk requiring mitigation

## XSS Attacks

XSS vulnerabilities enable a wide range of attacks executable through browser JavaScript, including:
- Stealing session cookies
- Executing unauthorized API calls (e.g., password changes)
- Bitcoin mining or ad injection
- Binary exploits through browser vulnerabilities
- Sandbox breakouts leading to system-level code execution

**Notable XSS examples:**
- **Samy Worm (2005):** MySpace stored XSS that infected over one million users in a day
- **Twitter TweetDeck (2014):** Self-retweeting exploit with 38,000+ retweets in two minutes
- **Google Search & Apache Server:** Recent vulnerabilities actively exploited for credential theft

## Types of XSS

| Type | Description |
|------|-------------|
| **Stored (Persistent) XSS** | User input stored in back-end database and displayed on retrieval (posts, comments) |
| **Reflected (Non-Persistent) XSS** | User input displayed after backend processing but not stored (search results, error messages) |
| **DOM-based XSS** | Non-persistent XSS where input is processed client-side without reaching the server (HTTP parameters, anchor tags) |

Each type will be explored in detail with practical exercises and attack scenarios.
