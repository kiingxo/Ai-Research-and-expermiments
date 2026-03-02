# Public Datasets & Repositories

## Hugging Face Datasets

**Use Case**: Pre-built, ready-to-use NLP datasets across multiple tasks

**Key Features**:
- 1000+ curated datasets
- Automatic download and caching
- Multi-language support
- Easy integration with transformers library

**Getting Started**:
```python
from datasets import load_dataset

# Load a popular dataset
dataset = load_dataset("glue", "mrpc")  # Microsoft Research Paraphrase Corpus

print(dataset)
# Shows splits: train, validation, test

# Access data
for example in dataset["train"].take(5):
    print(f"Sentence 1: {example['sentence1']}")
    print(f"Sentence 2: {example['sentence2']}")
    print(f"Label: {example['label']}\n")

# Stream large datasets without full download
dataset = load_dataset("wikitext", "wikitext-103-v1", split="train", streaming=True)
```

**Popular Datasets**:
- `glue` - General Language Understanding Evaluation
- `squad` - Extractive QA dataset
- `wmt14` - Machine translation
- `wikipedia` - Full Wikipedia corpus
- `common_voice` - Multilingual speech

**Cost**: Free
**Documentation**: https://huggingface.co/datasets

---

## Kaggle Datasets

**Use Case**: Diverse, community-curated datasets, competitions with datasets

**Key Features**:
- 100,000+ datasets
- Text classification, sentiment, NER datasets
- Competitions with labeled data
- Downloader API

**Getting Started**:
```python
# Install kaggle CLI
# pip install kaggle

# Configure credentials (~/.kaggle/kaggle.json)
from kaggle.api.kaggle_api_extended import KaggleApi

api = KaggleApi()
api.authenticate()

# Download dataset
api.dataset_download_files('dataset-owner/dataset-name', path='./data', unzip=True)

# Or use in Python
import pandas as pd
df = pd.read_csv('data/dataset.csv')
```

**Popular Datasets**:
- Amazon Reviews (sentiment)
- Twitter Sentiment
- News Category Dataset
- SMS Spam Collection

**Cost**: Free (with Kaggle account)
**Documentation**: https://www.kaggle.com/api

---

## Google Dataset Search

**Use Case**: Discovering datasets across the web

**Key Features**:
- Index of 25+ million datasets
- Find data from institutions, publishers, organizations
- Filter by license, format, date updated
- Provides metadata and access links

**Getting Started**:
```python
# Visit: https://datasetsearch.research.google.com/
# Search for your topic
# Filter by license (CC0, CC-BY, etc.)
# Download directly or follow links
```

**Cost**: Free
**Website**: https://datasetsearch.research.google.com/

---

## Wikipedia Dumps

**Use Case**: Large-scale monolingual text, language modeling pre-training

**Key Features**:
- Complete Wikipedia content
- Available for all languages
- Monthly updates
- Multiple formats (XML, bz2)

**Getting Started**:
```python
# Download via mwclient library
import mwclient
import gzip

site = mwclient.Site('en.wikipedia.org')

# Dump API
# Visit: https://dumps.wikimedia.org/

# Or use already-processed versions:
from datasets import load_dataset

wiki = load_dataset("wikipedia", "20220301.en")
print(wiki["train"][0])
```

**Cost**: Free
**Documentation**: https://dumps.wikimedia.org/

---

## BookCorpus

**Use Case**: Book text for language model pre-training, long-context modeling

**Key Features**:
- 11,000 books
- ~74 million sentences
- Free of copyright-heavy texts (mostly out of print)

**Getting Started**:
```python
from datasets import load_dataset

books = load_dataset("bookcorpus")

for example in books["train"].take(10):
    print(example["text"][:200] + "...\n")
```

**Cost**: Free
**Documentation**: https://huggingface.co/datasets/bookcorpus

---

## MNIST, CIFAR (and ImageNet for context)

**Use Case**: Multimodal learning, vision-language models

**Key Features**:
- Labeled image datasets
- Can be combined with descriptions for vision-NLP tasks

**Getting Started**:
```python
from datasets import load_dataset

# Load MNIST
mnist = load_dataset("mnist")

# For vision-language:
coco = load_dataset("coco")  # Images + captions
```

**Cost**: Free
**Note**: These are primarily vision datasets but useful for multimodal NLP

---

## Universal Dependencies

**Use Case**: Syntax annotation, dependency parsing, multilingual parsing

**Key Features**:
- Treebanks in 100+ languages
- Universal dependency annotations
- Standardized format across languages

**Getting Started**:
```python
from datasets import load_dataset

# Load UD English Web Treebank
ud_ewt = load_dataset("universal_dependencies", "en_ewt")

for example in ud_ewt["train"].take(3):
    print(f"Tokens: {example['tokens']}")
    print(f"Deps: {example['deps']}\n")
```

**Cost**: Free
**Documentation**: https://universaldependencies.org/

---

## COW (Corpora from the Web)

**Use Case**: Large web corpora in multiple languages

**Key Features**:
- Billions of words
- Multiple languages
- Linguistically processed

**Cost**: Free (with registration)
**Website**: https://corporafromtheweb.org/

---

## SQuAD (Stanford Question Answering Dataset)

**Use Case**: Extractive QA, reading comprehension, question generation

**Key Features**:
- 100K+ QA pairs
- Wikipedia articles as context
- Crowdsourced questions and answers

**Getting Started**:
```python
from datasets import load_dataset

squad = load_dataset("squad")

example = squad["train"][0]
print(f"Context: {example['context']}")
print(f"Question: {example['question']}")
print(f"Answer: {example['answers']}")
```

**Cost**: Free
**Documentation**: https://huggingface.co/datasets/squad

---

## GLUE & SuperGLUE

**Use Case**: Benchmark evaluation, multi-task learning

**Key Features**:
- 9 diverse NLU tasks (GLUE)
- Harder version with 8 tasks (SuperGLUE)
- Standard evaluation benchmark

**Cost**: Free
**Documentation**: https://huggingface.co/datasets/glue

---

## Recommendation by Task

| Task | Best Dataset | Alternative |
|------|--------------|-------------|
| Sentiment | Hugging Face GLUE | Kaggle Twitter Sentiment |
| QA | SQuAD | Hugging Face QuAC |
| Classification | Kaggle/GLUE | Hugging Face TREC |
| Translation | WMT14 | Kaggle parallel corpora |
| Summarization | CNN/DailyMail | Kaggle news datasets |
| Language Modeling | Wikipedia/BookCorpus | CommonCrawl |
| Parsing | Universal Dependencies | Penn Treebank |

---

## Dataset Discovery Workflow

1. **Hugging Face** → Start here for popular, clean datasets
2. **Kaggle** → Find competitions and unique datasets
3. **Google Dataset Search** → Discover institutional datasets
4. **ArXiv/Papers** → Find datasets from research papers
5. **GitHub** → Find community-curated datasets
6. **Create your own** → Use APIs above + annotation services
