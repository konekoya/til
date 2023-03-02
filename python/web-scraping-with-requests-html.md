Web Scraping with Requests HTML

[Beautifulsoup](https://pypi.org/project/beautifulsoup4/), combine with [requests](https://pypi.org/project/requests/) is very powerful for scraping data from static websites. However, if the content on a site is dynamically loaded via JavaScript, we will need to use tools such as [Selenium](https://www.selenium.dev/) or [requests-html](https://github.com/psf/requests-html). Here is a quick example that I put together using Python's request-html module.

```py
from requests_html import HTMLSession

session = HTMLSession()

url = 'https://github.com/konekoya'
r = session.get(url)
r.html.render()

# Get contribution count from my GitHub main page
el = r.html.find('#user-profile-frame .js-yearly-contributions h2')
print(el[0].text)
```
