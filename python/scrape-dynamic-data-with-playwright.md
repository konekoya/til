# Scrape Dynamic Data with Playwright

For scraping dynamic websites, you can use [Requests-HTML](dynamic-web-content-scraping-with-requests-html.md) to do so. But if that still can get the job done, you can consider using [playwright](https://playwright.dev/) - a headless browser to scrape the web content:

```py
from playwright.sync_api import sync_playwright
from selectolax.parser import HTMLParser


def parse_item(html_page):
    results = []
    html = HTMLParser(html_page)
    data = html.css("div.caption")

    for item in data:
        title = item.css_first("a.title").attributes["title"]
        results.append(title)
    return results


def main():
    url = "https://webscraper.io/test-sites/e-commerce/ajax/computers/laptops"
    with sync_playwright() as pw:
        browser = pw.chromium.launch(headless=False)
        page = browser.new_page()
        page.goto(url, wait_until="networkidle")
        next_page = page.locator(".next")

        while True:
            # A neat trick for scraping web content until it reaches the end of the pager
            if next_page.is_disabled():
                break

            page.click(".next")
            page.wait_for_load_state("networkidle")


if __name__ == "__main__":
    main()
```
