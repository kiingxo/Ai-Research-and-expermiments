# 2. NLP Fundamentals

Natural Language Processing concepts, datasets, and APIs for creating NLP datasets.

## Contents

- **apis/** - Comprehensive guide to public APIs and dataset sources
  - [social_media_apis.md](./apis/social_media_apis.md) - Twitter, Reddit, YouTube, etc.
  - [news_content_apis.md](./apis/news_content_apis.md) - NewsAPI, Guardian, PubMed, ArXiv
  - [public_datasets.md](./apis/public_datasets.md) - Hugging Face, Kaggle, Wikipedia, SQuAD
  - [speech_apis.md](./apis/speech_apis.md) - Common Voice, LibriSpeech, AudioSet
  - [specialized_apis.md](./apis/specialized_apis.md) - Domain-specific APIs (Medical, Finance, Legal)
  - [annotation_services.md](./apis/annotation_services.md) - Data labeling (Labelbox, Scale AI, MTurk)

## Key NLP Tasks

### Text Classification
- Sentiment analysis
- Topic classification
- Intent detection

### Sequence Labeling
- Named Entity Recognition (NER)
- Part-of-Speech (POS) tagging
- Chunking

### Structured Prediction
- Machine translation
- Question answering
- Semantic role labeling

### Understanding
- Reading comprehension
- Semantic similarity
- Textual entailment

## Dataset Quick Links

**Text Data**: [Social Media](./apis/social_media_apis.md) | [News](./apis/news_content_apis.md) | [Pre-built Datasets](./apis/public_datasets.md)

**Speech**: [Common Voice](./apis/speech_apis.md) | [LibriSpeech](./apis/speech_apis.md) | [AudioSet](./apis/speech_apis.md)

**Specialized**: [Academic](./apis/specialized_apis.md) | [Code](./apis/specialized_apis.md) | [Medical](./apis/specialized_apis.md)

**Labeling**: [Crowdsourced](./apis/annotation_services.md) | [Professional](./apis/annotation_services.md) | [Open Source](./apis/annotation_services.md)

## Recommended Learning Flow

1. **Start here**: Understand basic NLP tasks and challenges
2. **Explore APIs**: Find data sources relevant to your project
3. **Get datasets**: Use public datasets or APIs to collect data
4. **Label data**: Use annotation services if needed
5. **Build models**: Move to 3-training-techniques for implementation

## Quick Start

- Want to build a sentiment classifier? → See [social_media_apis.md](./apis/social_media_apis.md) for Twitter data
- Need a QA dataset? → See [public_datasets.md](./apis/public_datasets.md) for SQuAD
- Building multilingual model? → Check [speech_apis.md](./apis/speech_apis.md) for Common Voice
- Need to annotate data? → Reference [annotation_services.md](./apis/annotation_services.md)

## Next Steps

→ **3-training-techniques** - How to train NLP models
