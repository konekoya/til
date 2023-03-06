# Display Web Scraping Data with Pandas

Pandas is a very good tool for data analysis and parsing. It can also be useful when scraping data from the web, whether you want to view it in the terminal or save it as a .csv or .json file, among other formats.

```py
import pandas as pd
import requests
from bs4 import BeautifulSoup

# Logic for getting the product_links from the site...

whisky_list = []
for link in product_links:
    r = requests.get(link, headers=headers)
    soup = BeautifulSoup(r.content, "lxml")
    name = soup.select_one(".product-main__name").text.strip()
    price = soup.select_one(".product-action__price").text.strip()

    whisky = {
        "name": name,
        "rating": rating,
        "price": price
    }

    whisky_list.append(whisky)

# Here is the juicy part. You can use pandas to create a DataFrame with your data
df = pd.DataFrame(whisky_list)

# And display it with pandas :)
print(df.head(15))
```

The above will print out a beautiful tabular data in your terminal:

```
                                          name                 rating   price
0                               Hibiki Harmony    4\n\n\n(62 Reviews)  £76.95
1                         Yamazaki 12 Year Old  4.5\n\n\n(94 Reviews)    £139
2                    Nikka Coffey Grain Whisky  4.5\n\n\n(52 Reviews)  £57.95
3                 Yamazaki Distiller's Reserve  4.5\n\n\n(55 Reviews)  £72.95
4                             The Chita Whisky  4.5\n\n\n(42 Reviews)  £51.95
5                  Hakushu Distiller's Reserve  4.5\n\n\n(28 Reviews)  £70.95
6                           Yoichi Single Malt  4.5\n\n\n(10 Reviews)  £77.75
7                                 Suntory Toki    4\n\n\n(35 Reviews)  £33.95
8                        Miyagikyo Single Malt  4.5\n\n\n(10 Reviews)  £78.45
9             Kaiyo Mizunara Oak Cask Strength     5\n\n\n(3 Reviews)    £110
10                          Kaiyo Mizunara Oak     5\n\n\n(2 Reviews)  £82.95
11  The House of Suntory Triology Pack\n3x20cl              no rating  £44.95
12      Ichiro's Malt Double Distilleries 2021      2\n\n\n(1 Review)    £299
13   Akashi 5 Year Old\nSherry Cask Half Litre     5\n\n\n(2 Reviews)    £150
14  Shizuoka Contact S Single Malt\n3 Year Old              no rating    £175
```

Kudos to [John Watson Rooney](https://www.youtube.com/@JohnWatsonRooney) for this useful tip
