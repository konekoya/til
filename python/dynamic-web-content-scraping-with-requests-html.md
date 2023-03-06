# Dynamic Web Content Scraping with Requests HTML

[Beautifulsoup](https://pypi.org/project/beautifulsoup4/), combine with [requests](https://pypi.org/project/requests/) is very powerful for scraping data from static websites. However, if the content on a site is dynamically loaded via JavaScript, we will need to use tools such as [Selenium](https://www.selenium.dev/) or [requests-html](https://github.com/psf/requests-html). Here is a quick example that I put together using Python's requests-html module.

```py
from requests_html import HTMLSession

url = 'https://www.beerwulf.com/en-gb/c/all-beers?segment=Beers&catalogCode=Beer_1'

s = HTMLSession()
r = s.get(url)

# The sleep here is after the content is loaded. This will ensure the content is fully loaded and avoid problems when we start scraping the content
r.html.render(sleep=1)
products = r.html.xpath('//*[@id="product-items-container"]', first=True)

for item in products.absolute_links:
    r = s.get(item)
    name = r.html.find('.product-detail-info-title > h1', first=True).text
    subtext = r.html.find('.product-subtext > span', first=True).text
    print(name, subtext)
```

In the example above, the `HTMLSession` call will create a browser under the hood, so it will wait for the content to be loaded and from there start query the DOM elements and scraping the content that we want.
