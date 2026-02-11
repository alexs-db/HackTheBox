# Creepy Crawlies

Web crawling is vast and intricate, but you don't have to embark on this journey alone. A plethora of web crawling tools are available to assist you, each with its own strengths and specialties. These tools automate the crawling process, making it faster and more efficient, allowing you to focus on analyzing the extracted data.

## Popular Web Crawlers

- **Burp Suite Spider**: Burp Suite, a widely used web application testing platform, includes a powerful active crawler called Spider. Spider excels at mapping out web applications, identifying hidden content, and uncovering potential vulnerabilities.
- **OWASP ZAP (Zed Attack Proxy)**: ZAP is a free, open-source web application security scanner. It can be used in automated and manual modes and includes a spider component to crawl web applications and identify potential vulnerabilities.
- **Scrapy (Python Framework)**: Scrapy is a versatile and scalable Python framework for building custom web crawlers. It provides rich features for extracting structured data from websites, handling complex crawling scenarios, and automating data processing. Its flexibility makes it ideal for tailored reconnaissance tasks.
- **Apache Nutch (Scalable Crawler)**: Nutch is a highly extensible and scalable open-source web crawler written in Java. It's designed to handle massive crawls across the entire web or focus on specific domains. While it requires more technical expertise to set up and configure, its power and flexibility make it a valuable asset for large-scale reconnaissance projects.

> **Note**: Adhering to ethical and responsible crawling practices is crucial no matter which tool you choose. Always obtain permission before crawling a website, especially if you plan to perform extensive or intrusive scans. Be mindful of the website's server resources and avoid overloading them with excessive requests.

## Scrapy

We will leverage Scrapy and a custom spider tailored for reconnaissance on inlanefreight.com. For more information on crawling/spidering techniques, refer to the "Using Web Proxies" module.

### Installing Scrapy

```bash
pip3 install scrapy
```

### ReconSpider

Download and extract the custom Scrapy spider:

```bash
wget -O ReconSpider.zip https://academy.hackthebox.com/storage/modules/144/ReconSpider.v1.2.zip
unzip ReconSpider.zip
```

Run ReconSpider:

```bash
python3 ReconSpider.py http://inlanefreight.com
```

## results.json Output

The spider saves data to `results.json` with the following structure:

```json
{
    "emails": ["lily.floid@inlanefreight.com", "cvs@inlanefreight.com"],
    "links": ["https://www.themeansar.com", "https://www.inlanefreight.com/index.php/offices/"],
    "external_files": ["https://www.inlanefreight.com/wp-content/uploads/2020/09/goals.pdf"],
    "js_files": ["https://www.inlanefreight.com/wp-includes/js/jquery/jquery-migrate.min.js?ver=3.3.2"],
    "form_fields": [],
    "images": ["https://www.inlanefreight.com/wp-content/uploads/2021/03/AboutUs_01-1024x810.png"],
    "videos": [],
    "audio": [],
    "comments": ["<!-- #masthead -->"]
}
```

### JSON Keys

| Key | Description |
|-----|-------------|
| `emails` | Email addresses found on the domain |
| `links` | URLs of links found within the domain |
| `external_files` | URLs of external files (e.g., PDFs) |
| `js_files` | URLs of JavaScript files used by the website |
| `form_fields` | Form fields found on the domain |
| `images` | URLs of images found on the domain |
| `videos` | URLs of videos found on the domain |
| `audio` | URLs of audio files found on the domain |
| `comments` | HTML comments found in the source code |

By exploring this JSON structure, you can gain valuable insights into the web application's architecture, content, and potential points of interest for further investigation.
