# ZAP Scanner

ZAP includes a Web Scanner for building site maps via ZAP Spider and performing passive and active scans to identify vulnerabilities.

## Spider

ZAP Spider works like Burp's Crawler. Start a scan by:
- Right-clicking a request in History and selecting **Attack > Spider**
- Using the HUD in the pre-configured browser and clicking the Spider Start button

> **Note:** ZAP may prompt you to add the website to your scope before scanning. The Scope defines which URLs ZAP will test. You can customize it to scan multiple targets.

The Spider scans the website, follows links, and validates them. Monitor progress in the HUD or main ZAP UI. Once complete, view the Sites tab to see an expandable tree of discovered URLs and directories.

**Tip:** Use **Ajax Spider** (third button on right pane) after the normal Spider finishes. It identifies links from JavaScript AJAX requests, often finding additional targets.

## Passive Scanner

As ZAP Spider makes requests, it automatically runs the passive scanner on responses, identifying potential issues like missing security headers or DOM-based XSS vulnerabilities.

View alerts in:
- Left pane: Issues on the current page
- Right pane: Overall alerts across the application
- **Alerts tab** in main ZAP UI: All identified issues with affected pages

## Active Scanner

Click the **Active Scan** button to scan all discovered pages. If no Spider scan exists, ZAP runs it automatically.

The Active Scanner tests various attacks against all pages and HTTP parameters. This takes longer than passive scanning. As it runs, new alerts populate based on discovered vulnerabilities.

**High alerts** are critical—they typically lead to direct application or back-end compromise. Review alert details to understand the vulnerability and replication method.

## Reporting

Generate a report by selecting **Report > Generate HTML Report** from the top bar. Choose your save location and format (HTML, XML, or Markdown). The report displays all findings in an organized manner, useful for logging penetration test results.
