---
title: "Ch 12: Working with APIs & Web Scraping"
weight: 12
---

# Working with APIs & Web Scraping

## Learning Objectives

After reading this chapter, you will be able to:
- Make HTTP requests with the `requests` library
- Parse and consume REST API responses
- Authenticate with APIs (API keys, OAuth, JWT)
- Scrape websites using `BeautifulSoup` and `Scrapy`
- Handle rate limiting and pagination
- Build async API clients with `httpx`

---

## 12.1 HTTP Basics

### HTTP Methods

| Method | Purpose | REST Convention |
|--------|---------|----------------|
| `GET` | Retrieve data | Read resource |
| `POST` | Create new resource | Create |
| `PUT` | Update entire resource | Replace |
| `PATCH` | Partial update | Modify |
| `DELETE` | Remove resource | Delete |

### HTTP Status Codes

```
2xx Success:  200 OK, 201 Created, 204 No Content
3xx Redirect: 301 Moved Permanently, 304 Not Modified
4xx Client:   400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found
5xx Server:   500 Internal Server Error, 502 Bad Gateway, 503 Service Unavailable
```

---

## 12.2 The `requests` Library

```python
import requests

# GET request
response = requests.get("https://api.github.com/users/python")
print(response.status_code)   # 200
print(response.ok)            # True

# Response content
print(response.text)           # Raw string
print(response.json())         # Parsed JSON
print(response.headers)        # Response headers

# Query parameters
params = {"q": "python", "page": 1, "per_page": 10}
response = requests.get("https://api.github.com/search/repositories", params=params)
print(response.url)
# https://api.github.com/search/repositories?q=python&page=1&per_page=10

# POST with JSON
data = {"title": "New Issue", "body": "Description"}
response = requests.post(
    "https://api.github.com/repos/user/repo/issues",
    json=data,
    headers={"Authorization": "Bearer YOUR_TOKEN"}
)
print(response.status_code)  # 201 Created
print(response.json()["id"])  # New issue ID

# POST with form data
response = requests.post("https://httpbin.org/post", data={"key": "value"})

# PUT and DELETE
requests.put("https://api.example.com/resource/1", json={"name": "Updated"})
requests.delete("https://api.example.com/resource/1")
```

### Headers and Authentication

```python
import requests
from requests.auth import HTTPBasicAuth

# Custom headers
headers = {
    "User-Agent": "MyApp/1.0",
    "Accept": "application/json",
    "Authorization": "Bearer YOUR_API_TOKEN"
}
response = requests.get("https://api.example.com/data", headers=headers)

# Basic Authentication
response = requests.get(
    "https://api.example.com/secure",
    auth=HTTPBasicAuth("username", "password")
)

# Session (reuse connection, keep cookies)
session = requests.Session()
session.headers.update({"Authorization": "Bearer TOKEN"})

# All requests in this session use the same headers
resp1 = session.get("https://api.example.com/user")
resp2 = session.get("https://api.example.com/posts")
```

### Error Handling

```python
def fetch_data(url, timeout=10):
    try:
        response = requests.get(url, timeout=timeout)
        response.raise_for_status()  # Raises HTTPError for 4xx/5xx
        return response.json()
    except requests.exceptions.Timeout:
        print(f"Request to {url} timed out")
    except requests.exceptions.ConnectionError:
        print(f"Could not connect to {url}")
    except requests.exceptions.HTTPError as e:
        print(f"HTTP error: {e.response.status_code}")
    except requests.exceptions.RequestException as e:
        print(f"Unexpected error: {e}")
    return None
```

### Pagination Handling

```python
def fetch_all_pages(base_url, params=None):
    """Handle paginated API responses."""
    all_results = []
    page = 1
    
    while True:
        params = params or {}
        params["page"] = page
        
        response = requests.get(base_url, params=params)
        if not response.ok:
            break
        
        data = response.json()
        if not data:  # No more results
            break
        
        all_results.extend(data)
        page += 1
    
    return all_results
```

---

## 12.3 Working with REST APIs

### Complete API Client Example

```python
class GitHubClient:
    """A simple GitHub API client."""
    BASE_URL = "https://api.github.com"
    
    def __init__(self, token=None):
        self.session = requests.Session()
        self.session.headers.update({
            "Accept": "application/vnd.github.v3+json",
            "User-Agent": "Python-API-Client"
        })
        if token:
            self.session.headers["Authorization"] = f"token {token}"
    
    def get_user(self, username):
        resp = self.session.get(f"{self.BASE_URL}/users/{username}")
        resp.raise_for_status()
        return resp.json()
    
    def get_repos(self, username, sort="updated"):
        params = {"sort": sort, "per_page": 100}
        all_repos = []
        page = 1
        
        while True:
            params["page"] = page
            resp = self.session.get(
                f"{self.BASE_URL}/users/{username}/repos",
                params=params
            )
            resp.raise_for_status()
            repos = resp.json()
            if not repos:
                break
            all_repos.extend(repos)
            page += 1
        
        return all_repos
    
    def create_issue(self, repo_full_name, title, body=""):
        url = f"{self.BASE_URL}/repos/{repo_full_name}/issues"
        resp = self.session.post(url, json={"title": title, "body": body})
        resp.raise_for_status()
        return resp.json()

# Usage
client = GitHubClient(token="ghp_xxxxx")
user = client.get_user("python")
repos = client.get_repos("python")
print(f"User: {user['name']}, Public repos: {len(repos)}")
```

---

## 12.4 Rate Limiting and Backoff

```python
import time
import random

def fetch_with_retry(url, max_retries=3):
    for attempt in range(max_retries):
        response = requests.get(url)
        
        if response.status_code == 429:  # Too Many Requests
            retry_after = int(response.headers.get("Retry-After", 5))
            print(f"Rate limited. Waiting {retry_after}s...")
            time.sleep(retry_after)
            continue
        
        if response.status_code >= 500:  # Server error
            wait = 2 ** attempt + random.uniform(0, 1)
            print(f"Server error. Retrying in {wait:.2f}s...")
            time.sleep(wait)
            continue
        
        response.raise_for_status()
        return response.json()
    
    raise Exception("Max retries exceeded")
```

---

## 12.5 Web Scraping with BeautifulSoup

```python
from bs4 import BeautifulSoup
import requests

# Fetch and parse HTML
response = requests.get("https://example.com")
soup = BeautifulSoup(response.text, "html.parser")

# Find elements
print(soup.title.text)           # Page title
print(soup.find("h1").text)     # First h1

# Find all links
for link in soup.find_all("a"):
    print(link.get("href"), link.text)

# CSS selectors
posts = soup.select("div.blog-post")
for post in posts:
    title = post.select_one("h2 a")
    date = post.select_one(".date")
    if title:
        print(title.text, title.get("href"))

# Finding by class
items = soup.find_all(class_="product-item")

# Finding by attributes
images = soup.find_all("img", src=True)

# Get text (cleaned)
content = soup.get_text(separator=" ", strip=True)
```

### Scraping with Navigation

```python
def scrape_articles(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.content, "html.parser")
    
    articles = []
    for article in soup.find_all("article"):
        title_elem = article.find("h2")
        link_elem = title_elem.find("a") if title_elem else None
        summary_elem = article.find(class_="summary")
        
        articles.append({
            "title": title_elem.text.strip() if title_elem else None,
            "url": link_elem.get("href") if link_elem else None,
            "summary": summary_elem.text.strip() if summary_elem else None
        })
    
    return articles
```

### Handling JavaScript-Rendered Pages

```python
# Use requests-html (pip install requests-html)
from requests_html import HTMLSession

session = HTMLSession()
response = session.get("https://example.com")
response.html.render()  # Executes JavaScript!

# Now you can access dynamically-loaded content
items = response.html.find(".dynamic-content")
```

---

## 12.6 Web Scraping with Scrapy

```python
# spiders/article_spider.py
import scrapy

class ArticleSpider(scrapy.Spider):
    name = "articles"
    start_urls = ["https://blog.example.com"]
    
    def parse(self, response):
        # Extract articles from page
        for article in response.css("div.article"):
            yield {
                "title": article.css("h2::text").get(),
                "url": article.css("a::attr(href)").get(),
                "date": article.css(".date::text").get(),
            }
        
        # Follow pagination
        next_page = response.css("a.next::attr(href)").get()
        if next_page:
            yield response.follow(next_page, self.parse)

# Run: scrapy runspider article_spider.py -o articles.json
```

---

## 12.7 Async HTTP with `httpx`

```python
import httpx
import asyncio

async def fetch_url(url):
    async with httpx.AsyncClient() as client:
        response = await client.get(url)
        return response.json()

async def fetch_multiple(urls):
    async with httpx.AsyncClient() as client:
        tasks = [client.get(url) for url in urls]
        responses = await asyncio.gather(*tasks)
        return [r.json() for r in responses]

# Usage
urls = [
    "https://api.github.com/users/python",
    "https://api.github.com/users/microsoft",
    "https://api.github.com/users/google"
]
results = asyncio.run(fetch_multiple(urls))
print([r["login"] for r in results])
```

---

## Key Takeaways

- `requests` is the standard library for HTTP — use `Session()` for connection reuse
- Always handle errors with `raise_for_status()` and specific exception types
- Use `BeautifulSoup` or `Scrapy` for HTML parsing and web scraping
- Respect `robots.txt` and implement rate limiting when scraping
- For async API clients, use `httpx.AsyncClient`
- Pagination requires loops — check for next page links or cursor-based tokens
﻿

---

## Exercises

1. **Weather API**: Fetch weather data from OpenWeatherMap API and display it
2. **GitHub dashboard**: Use the GitHub API to show a user's repo stats
3. **Price tracker**: Scrape product prices from an e-commerce site
4. **Async scraper**: Scrape multiple URLs concurrently using `httpx`
5. **API wrapper**: Build a wrapper for a public API (e.g., SpaceX, Pokemon)
6. **RSS reader**: Parse an RSS feed using `feedparser` library

---

## Next Steps

→ Continue to [Chapter 13: Database & SQL Integration]({{< relref "13-database-and-sql-integration" >}})
