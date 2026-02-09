# Burp Scanner

An essential feature of web proxy tools is their web scanners. Burp Suite comes with Burp Scanner, a powerful scanner for various types of web vulnerabilities, using a Crawler for building the website structure, and Scanner for passive and active scanning.

Burp Scanner is a Pro-Only feature, and it is not available in the free Community version of Burp Suite. However, given the wide scope that Burp Scanner covers and the advanced features it includes, it makes it an enterprise-level tool, and as such, it is expected to be a paid feature.

## Target Scope

To start a scan in Burp Suite, you have the following options:
- Start scan on a specific request from Proxy History
- Start a new scan on a set of targets
- Start a scan on items in scope

### Adding Items to Scope

Right-click on a request in Proxy History or an item in the Site map and select **Add to scope** to include it in your scan.

### Managing Scope

To view and manage your scope, go to **Target > Scope**. You can:
- Add or remove items
- Use advanced scope control to specify regex patterns for inclusion/exclusion
- Exclude dangerous items (e.g., logout functions) by selecting **Remove from scope**

## Crawler

Once your scope is ready, go to **Dashboard** and click **New Scan** to configure a scan. Burp offers two scanning options:

1. **Crawl** - Maps the website structure by following links and examining requests
2. **Crawl and Audit** - Performs crawling followed by active scanning

> **Note:** Crawl scans only follow referenced links. They don't perform fuzzing to identify unreferenced pages like dirbuster or ffuf would. Use Burp Intruder or Content Discovery for that.

### Configuring a Crawl

Select a crawl configuration preset (e.g., "Crawl strategy - fastest") and optionally add credentials for authenticated scanning.

## Passive Scanner

A Passive Scan analyzes pages already visited without sending new requests. It identifies potential vulnerabilities like:
- Missing HTML tags
- DOM-based XSS vulnerabilities

**Limitations:** Only suggests potential vulnerabilities without verification. Use for quick analysis with confidence levels provided.

### Running a Passive Scan

Right-click on a request or target in the Site map and select **Do passive scan** or **Passively scan this target**.

## Active Scanner

The Active Scanner performs comprehensive vulnerability testing:

1. Runs crawl and web fuzzing to identify all pages
2. Executes a passive scan on identified pages
3. Verifies vulnerabilities with targeted requests
4. Performs JavaScript analysis
5. Fuzzes insertion points for XSS, SQL Injection, Command Injection, etc.

### Running an Active Scan

1. Go to **Dashboard > New Scan**
2. Select **Crawl and Audit**
3. Choose audit configuration preset (e.g., "Audit checks - critical issues only")
4. Click **Ok** to start

The scan may take longer depending on configurations. Monitor progress via the **Tasks** pane and review results in the **Logger** tab.

## Reporting

After scans complete, generate a report:

1. Go to **Target > Site map**
2. Right-click your target
3. Select **Issue > Report issues for this host**
4. Choose export type and details to include
5. View the organized report in your browser

Use these reports as supplementary data for your detailed client reports, not as standalone deliverables.
