[ HOME ](README.md)
# Read 17 - Web Scraping, AKA web harvesting, or web data extraction

> Web scraping is a technique to automatically access and extract large amounts of information from a website.
- It is a form of copying, in which specific data is gathered and copied from the web, typically into a central local database or spreadsheet, for later retrieval or analysis.
- Web scraping a web page involves fetching it and extracting from it.

## Steps
1. Figure out where we can locate the links to the files we want to download inside the multiple levels of HTML tags.
    1. On the website, right click and click on “Inspect”.
1. Import the following libraries.
```
import requests
import urllib.request
import time
from bs4 import BeautifulSoup
```
3. Set the url to the website and access the site with our requests library.
```
url = 'http://web.mta.info/developers/turnstile.html'
response = requests.get(url)
```
4. Parse the html with BeautifulSoup so that we can work with a nicer, nested data structure.
```
soup = BeautifulSoup(response.text, “html.parser”)
```

5. Use the method .findAll to locate all of our `<a>` tags.
```
soup.findAll('a')
```
6. Extract the actual link that we want.
```
one_a_tag = soup.findAll(‘a’)[36]
link = one_a_tag[‘href’]
```
7. We can use our urllib.request library to download this file path to our computer. We provide request.urlretrieve with two parameters: 
    1. file url and the 
    1. filename.
```
download_url = 'http://web.mta.info/developers/'+ link
urllib.request.urlretrieve(download_url,'./’'link[link.find('/turnstile_')+1:]) 
```
8. Last but not least, we should include this line of code so that we can pause our code for a second so that we are not spamming the website with requests.
```
time.sleep(1)
```

## Methods to prevent web scraping

- Blocking an IP address either manually or based on criteria such as geolocation and DNSRBL. This will also block all browsing from that address.
- Disabling any web service API that the website's system might expose.
- Bots sometimes declare who they are (using user agent strings) and can be blocked on that basis using robots.txt; 'googlebot' is an example. Other bots make no distinction between themselves and a human using a browser.- 
- Bots can be blocked by monitoring excess traffic.
- Bots can sometimes be blocked with tools to verify that it is a real person accessing the site, like a CAPTCHA. Bots are sometimes coded to explicitly break specific CAPTCHA patterns or may employ third-party services that utilize human labor to read and respond in real-time to CAPTCHA challenges.
- Commercial anti-bot services: Companies offer anti-bot and anti-scraping services for websites. A few web application firewalls have limited bot detection capabilities as well. However, many such solutions are not very effective.
- Locating bots with a honeypot or other method to identify the IP addresses of automated crawlers.
- Obfuscation using CSS sprites to display such data as phone numbers or email addresses, at the cost of accessibility to screen reader users.
- Because bots rely on consistency in the front-end code of a target website, adding small variations to the HTML/CSS surrounding important data and navigation elements would require more human involvement in the initial set up of a bot and if done effectively may render the target website too difficult to scrape due to the diminished ability to automate the scraping process.
- Websites can declare if crawling is allowed or not in the robots.txt file and allow partial access, limit the crawl rate, specify the optimal time to crawl and more.

____
# Tutorial

[Tutorial](https://www.youtube.com/watch?v=Bg9r_yLk7VY)