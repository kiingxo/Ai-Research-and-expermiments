# Specialized Domain APIs

## Academic & Research

### ArXiv API

**Use Case**: CS research papers, ML paper abstracts, dataset creation for academic NLP

**Key Features**:
- Millions of research papers
- Free full-text PDFs
- Searchable by category, date, author
- JSON/XML output format

**Getting Started**:
```python
import arxiv

# Simple search
client = arxiv.Client()

search = arxiv.Search(
    query='cat:cs.CL AND submittedDate:[202301010000 TO 202312312359]',
    max_results=100,
    sort_by=arxiv.SortCriterion.SubmittedDate
)

for result in client.results(search):
    print(f"Title: {result.title}")
    print(f"Authors: {result.authors}")
    print(f"Abstract: {result.summary}")
    print(f"PDF URL: {result.pdf_url}\n")

# Advanced search by subcategory
# cs.CL = Computation and Language
# cs.AI = Artificial Intelligence
# cs.LG = Machine Learning
```

**Cost**: Free
**Rate Limit**: 3 requests/second
**Documentation**: https://arxiv.org/help/api/

---

### PubMed API

**Use Case**: Biomedical text, medical NLP, clinical notes datasets

**Key Features**:
- 30+ million citations
- MeSH (Medical Subject Headings) indexing
- Free abstracts and metadata
- Full-text availability limited

**Getting Started**:
```python
from Bio import Entrez

# Set email for NCBI
Entrez.email = "your.email@example.com"

# Search
handle = Entrez.esearch(db="pubmed", term="natural language processing AND medicine", retmax=100)
record = Entrez.read(handle)
ids = record["IdList"]

# Fetch details
handle = Entrez.efetch(db="pubmed", id=",".join(ids), rettype="xml")
records = Entrez.read(handle)

for article in records["PubmedArticle"]:
    medline = article["MedlineCitation"]
    title = medline["Article"]["ArticleTitle"]
    abstract = medline["Article"].get("Abstract", {}).get("AbstractText", "N/A")
    
    print(f"Title: {title}")
    print(f"Abstract: {abstract}\n")
```

**Cost**: Free
**Rate Limit**: 3 requests/second
**Documentation**: https://www.ncbi.nlm.nih.gov/books/NBK25499/

---

### Google Scholar (via Unofficial APIs)

**Use Case**: Citation analysis, paper discovery, publication trends

**Key Features**:
- Citation counts
- Related papers
- Author profiles
- H-index

**Getting Started**:
```python
# Note: Official API limited, using community library
from scholarly import scholarly

# Search papers
search_query = scholarly.search_pubs("natural language processing")

for pub in search_query:
    print(f"Title: {pub['bib']['title']}")
    print(f"Citation Count: {pub['num_citations']}")
    print(f"Authors: {pub['bib']['author']}\n")
    if pub['num_citations'] > 100:
        break
```

**Cost**: Free (but unofficial)
**Rate Limit**: Be respectful (Google blocks aggressive scraping)
**Note**: Use official Google Scholar API when available

---

## Code & Programming

### GitHub API

**Use Case**: Code documentation, code-as-data for language models, variable naming patterns

**Key Features**:
- Search repositories and code
- File contents and metadata
- Repository statistics
- Commit history

**Getting Started**:
```python
import requests

GITHUB_TOKEN = "YOUR_GITHUB_TOKEN"
headers = {"Authorization": f"token {GITHUB_TOKEN}"}

# Search code
url = "https://api.github.com/search/code"
params = {
    "q": "language:python AND NLP",
    "per_page": 30,
    "sort": "stars"
}

response = requests.get(url, headers=headers, params=params)
results = response.json()["items"]

for item in results:
    print(f"File: {item['path']}")
    print(f"Repository: {item['repository']['full_name']}")
    print(f"Raw URL: {item['html_url']}\n")

# Get raw file content
raw_url = "https://raw.githubusercontent.com/owner/repo/main/file.py"
content = requests.get(raw_url).text
```

**Cost**: Free tier with rate limits
**Rate Limit**: 60 req/hour (unauthenticated), 5000 req/hour (authenticated)
**Documentation**: https://docs.github.com/en/rest?apiVersion=2022-11-28

---

### Stack Overflow API

**Use Case**: Q&A datasets, problem-solving conversations, code explanation pairs

**Key Features**:
- Questions and answers
- Tags and categories
- Vote scores and popularity
- User reputation

**Getting Started**:
```python
import requests

# Search questions
url = "https://api.stackexchange.com/2.3/search"
params = {
    "intitle": "python machine learning",
    "site": "stackoverflow",
    "sort": "votes",
    "order": "desc",
    "pagesize": 100
}

response = requests.get(url, params=params)
questions = response.json()["items"]

for q in questions:
    print(f"Title: {q['title']}")
    print(f"Score: {q['score']}")
    print(f"Answers: {q['answer_count']}")
    print(f"Tags: {q['tags']}\n")

# Get answer details
answer_url = f"https://api.stackexchange.com/2.3/questions/{q['question_id']}/answers"
answers = requests.get(answer_url, params={"site": "stackoverflow"}).json()["items"]
```

**Cost**: Free
**Rate Limit**: 300 requests/day
**Documentation**: https://api.stackexchange.com/docs

---

### Hugging Face Model Hub API

**Use Case**: Model cards, documentation, training scripts

**Key Features**:
- Access model metadata
- Download model information
- Search models by task
- Get training details

**Getting Started**:
```python
from huggingface_hub import HfApi, hf_hub_download

api = HfApi()

# List models
models = api.list_models(task="text-classification", limit=100)

for model in models:
    print(f"Model: {model.id}")
    print(f"Downloads: {model.downloads}")
    print(f"Likes: {model.likes}\n")

# Get model card
from huggingface_hub import ModelCard
card = ModelCard.load("bert-base-uncased")
print(card.content)  # Markdown content
```

**Cost**: Free
**Documentation**: https://huggingface.co/docs/hub/api

---

## Domain-Specific APIs

### Finance APIs

**Use Case**: Financial sentiment analysis, market NLP, earnings call transcripts

**Services**:
- **EDGAR** (SEC): Company filings, 10-K reports, earnings transcripts
- **Alpha Vantage**: Stock market data with news
- **NewsAPI Finance**: Financial news specifically

**Getting Started**:
```python
# SEC EDGAR
import requests

# Get company filings
company_ticker = "AAPL"
url = f"https://data.sec.gov/submissions/CIK{cik_number}.json"

# Financial news via NewsAPI
import requests

API_KEY = "YOUR_API_KEY"
response = requests.get(
    "https://newsapi.org/v2/everything",
    params={
        "q": "earnings",
        "category": "business",
        "language": "en",
        "apiKey": API_KEY
    }
)
articles = response.json()["articles"]
```

---

### Legal APIs

**Use Case**: Legal document analysis, contract NLP, case law datasets

**Services**:
- **Google Scholar (Law)**: Free case law and court opinions
- **Justia API**: Free legal research
- **OpenJurist**: Open-source legal database

**Cost**: Mostly free or freemium

---

### Medical/Clinical APIs

**Use Case**: Clinical note analysis, medical entity recognition, healthcare NLP

**Services**:
- **MIMIC Database**: De-identified clinical data (requires request)
- **ClinicalTrials.gov API**: Trial information and descriptions
- **ICD-10 APIs**: Medical coding datasets

**Cost**: Varies (MIMIC is research-grade and free)

---

## Comparison Table

| API | Domain | Volume | Auth | Cost |
|-----|--------|--------|------|------|
| ArXiv | Academic | Millions | Email | Free |
| PubMed | Biomedical | 30M+ | Email | Free |
| GitHub | Code | Massive | Token | Free+ |
| Stack Overflow | Q&A | Millions | No | Free |
| HuggingFace | ML Models | 100k+ | No | Free |
| SEC EDGAR | Finance | Hundreds K | No | Free |
| ClinicalTrials | Medical | 500k+ | No | Free |

---

## Recommendation by Domain

- **Computer Science**: ArXiv, GitHub, Hugging Face
- **Medicine**: PubMed, MIMIC, ClinicalTrials
- **Finance**: EDGAR, NewsAPI Finance, Yahoo Finance API
- **General Q&A**: Stack Overflow
- **Legal**: Google Scholar, Justia
