# Data Annotation & Labeling Services

## Overview

When you have raw data but need labels/annotations, these services help you crowdsource or manage labeling at scale.

---

## Labelbox

**Use Case**: Image, text, video, and 3D annotation for ML datasets

**Key Features**:
- Web-based annotation interface
- Supports multiple data types
- Team management and quality control
- API for integration
- Pre-built templates

**Getting Started**:
```python
from labelbox import Client

client = Client(api_key="YOUR_API_KEY")

# Create a dataset
dataset = client.create_dataset(name="NLP Dataset")

# Add data rows (text to annotate)
data_rows = [
    {"text": "This product is amazing!", "external_id": "review_1"},
    {"text": "Worst experience ever", "external_id": "review_2"},
]

dataset.create_data_rows(data_rows)

# Create annotation task
project = client.create_project(
    name="Sentiment Analysis",
    dataset_id=dataset.uid
)

# Get annotated results
annotations = project.get_label()
```

**Cost**: Starts ~$5K+/year (enterprise pricing)
**Best For**: Complex annotations, quality assurance, larger teams
**Supported Formats**: Text, images, video, 3D, PDF
**Documentation**: https://docs.labelbox.com/

---

## Scale AI

**Use Case**: High-quality human-labeled datasets for AI

**Key Features**:
- Expert annotators
- Custom annotation tasks
- Quality guarantees
- Fully managed service
- API-based workflow

**Getting Started**:
```python
import scale

client = scale.Client(api_key="YOUR_API_KEY")

# Create annotation task
task = client.create_categorization_task(
    project="my_nlp_project",
    callback_url="https://mysite.com/callback",
    instruction="Classify the sentiment of this review",
    attachment_type="text",
    attachment="This phone is terrible",
    categories=["positive", "negative", "neutral"]
)

# Retrieve results
task_id = task.task_id
status = client.get_task(task_id)
print(f"Status: {status.status}")
print(f"Result: {status.response}")
```

**Cost**: Variable (annotation-dependent), typically $0.10-1.00+ per item
**Best For**: High-quality, expert annotations
**Turnaround**: 24-48 hours typically
**Documentation**: https://docs.scale.com/

---

## AWS Mechanical Turk (MTurk)

**Use Case**: Large-scale crowdsourced annotations, cost-effective labeling

**Key Features**:
- Global workforce
- Pay-per-task model
- Built-in quality control
- Qualification system for workers
- Python SDK available

**Getting Started**:
```python
import boto3

# Initialize MTurk client
mturk = boto3.client(
    'mturk-requester',
    endpoint_url='https://mturk-requester.us-east-1.amazonaws.com',
    region_name='us-east-1'
)

# Create HIT (Human Intelligence Task)
question_xml = '''
<QuestionForm xmlns="http://mechanicalturk.amazonaws.com/AWSMechanicalTurkDataSchemas/2005-10-01/QuestionForm.xsd">
    <Question>
        <QuestionIdentifier>sentiment</QuestionIdentifier>
        <QuestionContent>
            <Text>What is the sentiment of this review?</Text>
            <Text>"Great product, highly recommend!"</Text>
        </QuestionContent>
        <AnswerSpecification>
            <SelectionAnswer>
                <StyleSuggestion>radioButton</StyleSuggestion>
                <Selections>
                    <Selection>
                        <SelectionIdentifier>positive</SelectionIdentifier>
                        <Text>Positive</Text>
                    </Selection>
                    <Selection>
                        <SelectionIdentifier>negative</SelectionIdentifier>
                        <Text>Negative</Text>
                    </Selection>
                    <Selection>
                        <SelectionIdentifier>neutral</SelectionIdentifier>
                        <Text>Neutral</Text>
                    </Selection>
                </Selections>
            </SelectionAnswer>
        </AnswerSpecification>
    </Question>
</QuestionForm>
'''

# Create task
response = mturk.create_hit(
    Title='Sentiment Classification',
    Description='Classify the sentiment of customer reviews',
    Keywords='sentiment,classification,nlp',
    Reward='0.10',
    MaxAssignments=3,
    LifetimeInSeconds=172800,
    Question=question_xml,
    QualificationRequirements=[
        {
            'QualificationTypeId': '000000000000000000L0',
            'Comparator': 'GreaterThanOrEqualTo',
            'IntegerValues': [95]  # 95% approval rating
        }
    ]
)

hit_id = response['HIT']['HITId']
print(f"HIT Created: {hit_id}")

# Get results
assignments = mturk.list_assignments_for_hit(HITId=hit_id)
```

**Cost**: Very low ($0.01-0.50+ per task depending on complexity)
**Best For**: Large-scale, budget-conscious projects
**Workforce**: 500,000+ global workers
**Quality**: Variable (use qualifications and bonuses to ensure quality)
**Documentation**: https://docs.aws.amazon.com/AWSMechTurk/

---

## Prodigy

**Use Case**: Active learning, iterative annotation, smaller-scale projects

**Key Features**:
- Python-based annotation tool
- Active learning integration
- Runs locally or in cloud
- Keyboard shortcuts for speed
- Lightweight

**Getting Started**:
```python
# Installation
# pip install prodigy

# Command line interface
# prodigy textcat.manual my-dataset data.jsonl --label positive,negative,neutral

# Python integration
from prodigy.components.loaders import JSONL

# Load data
stream = JSONL("reviews.jsonl")

# Configure annotation task
config = {
    "view_id": "classification",
    "labels": ["positive", "negative", "neutral"],
    "exclude_by": "input"  # Avoid duplicate reviews
}
```

**Cost**: One-time license (~$390)
**Best For**: Research, small-medium teams, active learning workflows
**Data Storage**: Local or cloud
**Documentation**: https://prodi.gy/

---

## LabelImg & Similar Open Source Tools

**Use Case**: Free, self-hosted annotation

**Key Features**:
- Completely free and open-source
- Self-hosted (no data leaves your server)
- No per-item costs
- Limited features vs. commercial tools

**Options**:
- **LabelImg**: Image bounding boxes
- **Doccano**: Text classification, NER, sequence labeling
- **CVAT**: Comprehensive annotation platform
- **VoTT**: Video and image object tagging

**Getting Started with Doccano**:
```bash
# Installation
pip install doccano

# Run locally
doccano init
doccano start

# Access at http://localhost:8000
```

**Cost**: Free
**Best For**: Budget projects, private data, experimentation
**Documentation**: https://github.com/doccano/doccano

---

## Comparison Table

| Service | Cost | Scale | Speed | Quality | Best For |
|---------|------|-------|-------|---------|----------|
| Labelbox | $5K+/year | Large | Fast | High | Enterprise, complex tasks |
| Scale AI | $0.10-1/item | Any | 24-48h | Very High | Expert annotations |
| MTurk | $0.01-0.50/item | Very Large | Hours-Days | Variable | Budget, volume |
| Prodigy | $390 one-time | Small-Medium | Real-time | User-driven | Research, active learning |
| Doccano | Free | Small-Medium | Manual | User-driven | Budget, internal teams |
| CVAT | Free | Small-Medium | Manual | User-driven | Vision + text, self-hosted |

---

## Workflow by Scenario

### Scenario 1: Large-Scale Commercial Project
1. Use **MTurk** for initial bulk annotation (cost-effective)
2. Use **Scale AI** for review/refinement (high quality)
3. Implement **active learning** in production

### Scenario 2: Research Project with Budget
1. Use **Prodigy** with active learning
2. Annotate ~500-1000 samples manually
3. Train model and iterate

### Scenario 3: Enterprise Project
1. Use **Labelbox** for complete workflow
2. Team management and QA built-in
3. Scale to millions of items

### Scenario 4: Startup/Budget-Conscious
1. Start with **Doccano** (free, self-hosted)
2. Annotation done by team
3. Use **MTurk** when budget allows

---

## Annotation Best Practices

✅ **Do**:
- Define clear annotation guidelines
- Start with small pilot
- Calculate inter-annotator agreement (Cohen's Kappa, Fleiss Kappa)
- Use quality control mechanisms (agreement checks)
- Pay fairly and appreciate workers
- Version control your guidelines as you refine

❌ **Don't**:
- Skip the pilot phase
- Expect 100% agreement
- Pay too little (affects quality)
- Change instructions mid-project
- Ignore worker feedback
- Assume crowdworkers are lazy (they're not)

---

## Inter-Annotator Agreement Metrics

```python
from sklearn.metrics import cohen_kappa_score, agreement
import pandas as pd

# Example: 2 annotators, 100 samples
annotator1 = [0, 1, 0, 1, 2, ...]  # 0=negative, 1=neutral, 2=positive
annotator2 = [0, 1, 1, 1, 2, ...]

# Cohen's Kappa (2 annotators)
kappa = cohen_kappa_score(annotator1, annotator2)
print(f"Cohen's Kappa: {kappa}")
# >0.8 = excellent, 0.6-0.8 = good, <0.4 = poor

# Fleiss' Kappa (3+ annotators)
from statsmodels.stats.inter_rater import fleiss_kappa
kappas = fleiss_kappa(annotation_matrix)
```

**Interpretation**:
- **0.81-1.00**: Almost perfect agreement
- **0.61-0.80**: Substantial agreement
- **0.41-0.60**: Moderate agreement
- **0.21-0.40**: Fair agreement
- **<0.20**: Slight agreement

---

## Cost Estimation

For 10,000 samples:
- **MTurk**: ~$500-5,000
- **Scale AI**: ~$2,000-10,000
- **Labelbox**: Included in subscription
- **Prodigy**: $390 (one-time) + time
- **Doccano**: Free + time
