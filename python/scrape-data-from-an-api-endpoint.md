# Scrape Data From an API Endpoint

This is a really cool technique that I learned from [John Watson](https://www.youtube.com/watch?v=8980WHjsC6E&list=PLRzwgpycm-Fio7EyivRKOBN4D3tfQ_rpu&index=5&ab_channel=JohnWatsonRooney). Usually, when a website's content is dynamically loaded with JavaScript to some API calls. We can scrape the data via Selenium or [Requests-HTML](dynamic-web-content-scraping-with-requests-html.md). However, there's another way to scrape the data that is faster and more robust with the help of Chrome DevTools and Postman.

Start from copying the request as cURL from Chrome's devTools:

![Screenshot 2023-03-07 at 3.26.41 pm image](https://i.imgur.com/6APP844.png)

Then, start Postman and import the cURL content as a new request:

![Screenshot 2023-03-07 at 3.27.57 pm image](https://i.imgur.com/MzJR0IJ.png)

You can test the request and see if the correct data is being fetched. And use Postman's code snippet to obtain a version that uses Python requests. With some small tweaks, we now have a working scraper:

```py
import pandas as pd
import requests

url = "https://api.afl.com.au/cfs/afl/wagering?application=Web"

headers = {
    'sec-ch-ua': '"Chromium";v="110", "Not A(Brand";v="24", "Brave";v="110"',
    'x-media-mis-token': '478bc88325a7c9378248717fcf8f2495',
    'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8',
    'Referer': 'https://www.afc.com.au/',
    'sec-ch-ua-mobile': '?0',
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/110.0.0.0 Safari/537.36',
    'sec-ch-ua-platform': '"macOS"'
}

r = requests.get(url, headers=headers)
data = r.json()

df = pd.json_normalize(data['competition']['books'])
print(df.head(20))
```

And the above will output the following:

```
        id                               name                     closeTime  ... displayInApp displayInAppIOS displayInAppAndroid
0  6990496                 Richmond v Carlton  2023-03-16T08:20:00.000+0000  ...         True            True                True
1  6990497              Geelong v Collingwood  2023-03-17T08:40:00.000+0000  ...         True            True                True
2  6990499       North Melbourne v West Coast  2023-03-18T02:45:00.000+0000  ...         True            True                True
3  6990500           Port Adelaide v Brisbane  2023-03-18T05:35:00.000+0000  ...         True            True                True
4  6990502       Melbourne v Western Bulldogs  2023-03-18T08:25:00.000+0000  ...         True            True                True
5  6990501                Gold Coast v Sydney  2023-03-18T09:00:00.000+0000  ...         True            True                True
6  6990504  Greater Western Sydney v Adelaide  2023-03-19T02:10:00.000+0000  ...         True            True                True
7  6990503                Hawthorn v Essendon  2023-03-19T04:20:00.000+0000  ...         True            True                True
8  6990505               St Kilda v Fremantle  2023-03-19T05:40:00.000+0000  ...         True            True                True
9  6793496        AFL Premiership Winner 2023  2023-09-30T10:00:00.000+0000  ...         True            True                True
```
