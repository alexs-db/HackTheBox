# Crawling

Crawling, often called spidering, is the automated process of systematically browsing the World Wide Web. Similar to how a spider navigates its web, a web crawler follows links from one page to another, collecting information. These crawlers are bots that use pre-defined algorithms to discover and index web pages for search engines, data analysis, or web reconnaissance.

## How Web Crawlers Work

A web crawler starts with a seed URL (initial web page), fetches and parses its content, extracts all links, and adds them to a queue for iterative crawling. Depending on configuration, it can explore an entire website or vast portions of the web.

### Example Structure

```
Homepage
├── link1
├── link2
└── link3

link1 Page
├── Homepage
├── link2
├── link4
└── link5
```

The crawler continues following links systematically, distinguishing crawling from fuzzing (guessing potential links).

## Crawling Strategies

### Breadth-First Crawling

Explores a website's width before depth. Crawls all links on the seed page, then moves to links on those pages. Useful for obtaining a broad overview of website structure.

### Depth-First Crawling

Prioritizes depth over breadth. Follows a single path as far as possible before backtracking. Useful for finding specific content or reaching deep pages.

## Extracting Valuable Information

Crawlers extract diverse data types:

- **Links (Internal & External)**: Map website structure and discover hidden pages
- **Comments**: Reveal sensitive details or vulnerability hints
- **Metadata**: Page titles, descriptions, keywords, authors, dates provide context
- **Sensitive Files**: Backup files (.bak, .old), configurations (web.config, settings.php), logs exposing credentials or API keys

## The Importance of Context

Individual data points gain significance when combined. A comment mentioning a software version, combined with outdated metadata or vulnerable configurations, indicates potential vulnerabilities. Contextual analysis—connecting dots across multiple findings—reveals the target's complete digital landscape and hidden security risks.
