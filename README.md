from bs4 import BeautifulSoup as bs
import pandas as pd
pd.set_option('display.max_colwidth', 500)
import time
import requests
import rando
page = requests.get("http://quotes.toscrape.com/")
page
# <Response [200]>
soup = bs(page.content)
soup
quotes = [i.text for i in soup.find_all(class_='text')]
quotes
authors = [i.text for i in soup.find_all(class_='author')]
urls=[f"http://quotes.toscrape.com/page/{i}/" for i in range(1,11)]
urls
time.sleep(random.choice(rate))# List of Authors and Quotes
authors = []

quotes = []

# List of URLs
urls = [f"http://quotes.toscrape.com/page/{i}/" for i in range(1,11)]

# List for Randomizing our request rate
rate = [i/10 for i in range(10)]

# Iterating through the URLS
for url in urls:
    
    # Accessing the Webpage
    page = requests.get(url)
    
    # Getting the webpage's content in pure html
    soup = bs(page.content)

    # Adding the authors and quotes to their lists
    authors.extend([i.text for i in soup.find_all(class_='author')])

    quotes.extend([i.text for i in soup.find_all(class_='text')])

    # Checking to see if we hit our required number of quotes then breaking the loop
    if len(quotes) >= 52:
        break
        
    # Randomizing our request rate    
    time.sleep(random.choice(rate))
