# WEB SCRAPING
#### <i>Welcome to Web Scraping in this blog we are going to cover some useful content on web scraping enjoy as you go through hope you get to learn something.</i>

## lets get started
Web scraping is the process of extracting data from websites. Beautiful Soup is a Python library used to parse HTML and XML documents and makes it easy to scrape information from web pages. Below, I’ll guide you through the basics of web scraping using Beautiful Soup, including installation, basic usage, and a sample script.

### Step 1: Installation
Before you can start using Beautiful Soup, you need to install it along with the requests library, which allows you to download web pages. You can install both using pip:
```.bash
pip install beautifulsoup4
pip install requests
```
### Step 2: Importing Libraries
```.py
from bs4 import BeautifulSoup
import requests
```
### Step 3: Fetching a Web Page
To scrape a web page, you first need to download its content using the requests library.

```.py
url = "https://example.com"
response = requests.get(url)

# Check if the request was successful
if response.status_code == 200:
    html_content = response.text
else:
    print("Failed to retrieve the web page")
```
### Step 4: Parsing the HTML Content
Once you have the HTML content, you can parse it using Beautiful Soup.

```.py
soup = BeautifulSoup(html_content, 'html.parser')
```

