## Web scraping with requests

For scraping static websites, [Requests](https://pypi.org/project/requests/) and [Beautiful Soup](<(https://pypi.org/project/beautifulsoup4/)>) are the go to libraries for me.

It's worth noting that if the data you're trying to scrape are dynamically loaded through JavaScript or APIs, then this method won't work.

```py
import requests
from bs4 import BeautifulSoup

url = "https://konekoya.github.io"

html_content = requests.get(url).text
soup = BeautifulSoup(html_content, "html.parser")

# We can use CSS selectors
el = soup.select_one(".avatar__title")
print(el.getText()) # Joshua

# Or by its attributes
img = soup.find("img", {"class", "avatar__img"})
print(img["alt"]) # Joshua's Picture
```

More example code can be found in the [official docs](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
