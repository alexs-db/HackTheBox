# robots.txt

Imagine you're a guest at a grand house party. While you're free to mingle and explore, there might be certain rooms marked "Private" that you're expected to avoid. This is akin to how robots.txt functions in the world of web crawling. It acts as a virtual "etiquette guide" for bots, outlining which areas of a website they are allowed to access and which are off-limits.

## What is robots.txt?

Technically, robots.txt is a simple text file placed in the root directory of a website (e.g., `www.example.com/robots.txt`). It adheres to the Robots Exclusion Standard, guidelines for how web crawlers should behave when visiting a website. This file contains instructions in the form of "directives" that tell bots which parts of the website they can and cannot crawl.

## How robots.txt Works

The directives in robots.txt typically target specific user-agents, which are identifiers for different types of bots. For example:

```txt
User-agent: *
Disallow: /private/
```

This directive tells all user-agents (`*` is a wildcard) that they cannot access any URLs starting with `/private/`. Other directives can allow access to specific directories, set crawl delays, or provide sitemap links.

## robots.txt Structure

The robots.txt file is a plain text document in the root directory. Each "record" is separated by a blank line and consists of:

- **User-agent**: Specifies which crawler the rules apply to. A wildcard (`*`) applies to all bots.
- **Directives**: Specific instructions for the identified user-agent.

### Common Directives

| Directive | Description | Example |
|-----------|-------------|---------|
| Disallow | Paths the bot should not crawl | `Disallow: /admin/` |
| Allow | Paths explicitly permitted | `Allow: /public/` |
| Crawl-delay | Delay between requests (seconds) | `Crawl-delay: 10` |
| Sitemap | URL to XML sitemap | `Sitemap: https://www.example.com/sitemap.xml` |

## Why Respect robots.txt?

While not strictly enforceable, legitimate crawlers respect robots.txt for:

- **Server Protection**: Prevents excessive traffic that could slow or crash servers
- **Information Security**: Shields sensitive data from search engine indexing
- **Legal Compliance**: Ignoring directives may violate terms of service or laws

## robots.txt in Web Reconnaissance

For security professionals, robots.txt is valuable intelligence:

- **Uncovering Hidden Directories**: Disallowed paths often point to sensitive information or administrative panels
- **Mapping Website Structure**: Reveals sections not linked in main navigation
- **Detecting Crawler Traps**: Identifies honeypot directories that indicate security awareness

## Example Analysis

```txt
User-agent: *
Disallow: /admin/
Disallow: /private/
Allow: /public/

User-agent: Googlebot
Crawl-delay: 10

Sitemap: https://www.example.com/sitemap.xml
```

This robots.txt indicates:
- All bots cannot access `/admin/` and `/private/` directories
- All bots can access `/public/`
- Googlebot must wait 10 seconds between requests
- Sitemap is available for efficient crawling

By analyzing this file, we can infer the website has an admin panel and private content in protected directories.
