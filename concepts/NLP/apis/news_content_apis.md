# News & Content APIs

## NewsAPI

**Use Case**: Sentiment analysis, topic extraction, news categorization, summarization models

**Key Features**:
- Search articles across thousands of news sources
- Filter by keywords, language, country, category, date
- Get headlines and full article summaries

**Getting Started**:
```python
import requests

API_KEY = "YOUR_API_KEY"
url = "https://newsapi.org/v2/everything"

params = {
    "q": "artificial intelligence",
    "sortBy": "publishedAt",
    "language": "en",
    "pageSize": 100,
    "apiKey": API_KEY
}

response = requests.get(url, params=params)
articles = response.json()["articles"]

for article in articles:
    print(f"Title: {article['title']}")
    print(f"Content: {article['content']}\n")
```

**Rate Limits**: 100 requests/day (free), higher for paid plans
**Cost**: Free tier available ($0-$449+/month for premium)
**Documentation**: https://newsapi.org/docs

---

## Medium API

**Use Case**: Long-form content analysis, topic modeling, writing style datasets

**Key Features**:
- Access published articles
- Get user publications and articles
- Limited official API (community alternatives exist)

**Getting Started**:
```python
import requests

# Using Medium RSS feed (alternative to official API)
feed_url = "https://medium.com/feed/@username"

import feedparser
feed = feedparser.parse(feed_url)

for entry in feed.entries:
    print(f"Title: {entry.title}")
    print(f"Content: {entry.summary}\n")
```

**Alternative**: Use web scraping with BeautifulSoup for articles
**Cost**: Free (with terms of service respect)
**Documentation**: https://github.com/Medium/medium-api-docs

---

## Guardian API

**Use Case**: News content analysis, topic classification, temporal trends

**Key Features**:
- Access articles from The Guardian
- Filter by section, date, keywords
- Get article metadata and content

**Getting Started**:
```python
import requests

API_KEY = "YOUR_API_KEY"
url = "https://open-platform.theguardian.com/search"

params = {
    "q": "technology",
    "api-key": API_KEY,
    "page-size": 50
}

response = requests.get(url, params=params)
results = response.json()["response"]["results"]

for article in results:
    print(f"Title: {article['webTitle']}")
    print(f"URL: {article['webUrl']}\n")
```

**Rate Limits**: 5,000 requests/day (free)
**Cost**: Free
**Documentation**: https://open-platform.theguardian.com/documentation/

---

## New York Times API

**Use Case**: News archives, domain-specific text, temporal language evolution

**Key Features**:
- Search articles from 1981 to present
- Article search with advanced filters
- Most popular articles
- Book reviews, movie reviews

**Getting Started**:
```python
import requests

API_KEY = "YOUR_API_KEY"
url = "https://api.nytimes.com/svc/search/v2/articlesearch.json"

params = {
    "q": "machine learning",
    "api-key": API_KEY,
    "page": 0,
    "sort": "newest"
}

response = requests.get(url, params=params)
articles = response.json()["response"]["docs"]

for article in articles:
    print(f"Title: {article['headline']['main']}")
    print(f"Abstract: {article['abstract']}\n")
```

**Rate Limits**: 4,000 requests/hour (free tier)
**Cost**: Free tier available
**Documentation**: https://developer.nytimes.com/

---

## CommonCrawl

**Use Case**: Web-scale text corpora, diverse language datasets, domain-specific data

**Key Features**:
- Freely available web crawl data
- Indexed by date (monthly snapshots)
- Access to petabytes of web content
- Available on AWS S3

**Getting Started**:
```python
from warcio.archiveiterator import ArchiveIterator
import requests

# List available crawls
response = requests.get("http://index.commoncrawl.org/collinfo.json")
crawls = response.json()

# Query a specific crawl
crawl_index = "https://index.commoncrawl.org/CC-MAIN-2024-10-index"
search_params = {"url": "*.example.com/*", "output": "json"}

response = requests.get(crawl_index, params=search_params)
for line in response.iter_lines():
    record = json.loads(line)
    print(record)
```

**Rate Limits**: None (but be respectful)
**Cost**: Free (AWS data transfer costs may apply)
**Documentation**: https://commoncrawl.org/get-started/

---

## ArXiv API

**Use Case**: Academic text, research abstracts, paper summarization

**Key Features**:
- Search academic papers
- Filter by category, date, author
- Get paper metadata and abstracts

**Getting Started**:
```python
import arxiv

# Search papers
client = arxiv.Client()
search = arxiv.Search(
    query='cat:cs.CL AND submittedDate:[202301010000 TO 202401010000]',
    max_results=100,
    sort_by=arxiv.SortCriterion.SubmittedDate
)

for result in client.results(search):
    print(f"Title: {result.title}")
    print(f"Abstract: {result.summary}\n")
```

**Rate Limits**: Reasonable limits (3 requests/second)
**Cost**: Free
**Documentation**: https://arxiv.org/help/api/

---

## PubMed API

**Use Case**: Biomedical text, medical NLP tasks, domain-specific language models

**Key Features**:
- Access millions of biomedical literature abstracts
- Search by keywords, MeSH terms, dates
- Get article metadata and abstracts

**Getting Started**:
```python
from Bio import Entrez

Entrez.email = "your.email@example.com"

# Search PubMed
search_handle = Entrez.esearch(db="pubmed", term="machine learning in healthcare", retmax=100)
search_results = Entrez.read(search_handle)
ids = search_results["IdList"]

# Fetch full records
fetch_handle = Entrez.efetch(db="pubmed", id=",".join(ids), rettype="xml")
records = Entrez.read(fetch_handle)

for article in records["PubmedArticle"]:
    title = article["MedlineCitation"]["Article"]["ArticleTitle"]
    abstract = article["MedlineCitation"]["Article"].get("Abstract", {})
    print(f"Title: {title}")
    print(f"Abstract: {abstract}\n")
```

**Rate Limits**: 3 requests/second (free)
**Cost**: Free
**Documentation**: https://www.ncbi.nlm.nih.gov/books/NBK25499/

---

## Comparison Table

| API | Domain | Volume | Cost | Auth | Rate Limit |
|-----|--------|--------|------|------|------------|
| NewsAPI | General News | Very High | Free+ | Required | 100/day |
| Medium | Long-form | High | Free | Optional | RSS feed |
| Guardian | News | High | Free | Required | 5k/day |
| NYT | Premium News | High | Free+ | Required | 4k/hour |
| CommonCrawl | Web Content | Massive | Free | No | Respectful |
| ArXiv | Academic | High | Free | No | 3/sec |
| PubMed | Biomedical | Very High | Free | Email | 3/sec |

---

## Recommendation by Use Case

- **General sentiment analysis**: NewsAPI, Guardian
- **Research/Academic**: ArXiv, PubMed
- **Trending topics**: NewsAPI, Medium
- **Web-scale datasets**: CommonCrawl
- **Domain-specific**: Choose by domain (Medical→PubMed, Academic→ArXiv)
