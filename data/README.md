# Data Management

Directory for datasets used in research and projects.

## Organization

- **raw/** - Original, unprocessed data
- **processed/** - Cleaned, transformed data
- **external/** - Downloaded datasets from APIs/sources
- **README.md** - Data documentation

## Data Collection Guidelines

### From APIs
See [2. NLP Fundamentals → APIs](../concepts/2-nlp-fundamentals/apis/) for complete guides:
- Social media APIs (Twitter, Reddit, YouTube)
- News and content APIs (NewsAPI, Guardian, PubMed)
- Public datasets (Hugging Face, Kaggle, Wikipedia)
- Speech/audio datasets
- Annotation services for labeling

### Local Storage Best Practices

```
data/
├── raw/
│   ├── twitter_raw_tweets.csv
│   └── emails_raw.jsonl
├── processed/
│   ├── twitter_processed_tokens.pkl
│   └── emails_cleaned.csv
└── external/
    ├── huggingface_glue/
    └── wikipedia_dump/
```

### Data Documentation
For each dataset, create a `DATASHEET.md`:
```markdown
# Dataset Name

## Source
- Where it came from
- Date collected
- Collection method

## Composition
- Number of examples
- Data types/format
- Label distribution

## Preprocessing
- Steps applied
- Filtering criteria
- Transformations

## Issues
- Missing values
- Biases
- Known problems
```

## Privacy & Ethics
- Anonymize PII before storing
- Respect terms of service
- Document consent/licensing
- Keep raw data secure
- Version control only metadata

## Size Considerations
- Use `.gitignore` for large files
- Store large datasets externally
- Use DVC or Git LFS for versioning
- Document download instructions
