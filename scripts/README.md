# Scripts & Utilities

Reusable automation scripts and utility functions for common tasks.

## Organization

```
scripts/
├── data_processing/
│   ├── preprocess_text.py
│   ├── tokenize.py
│   └── augment_data.py
│
├── training/
│   ├── train_classifier.py
│   ├── finetune_lm.py
│   └── distributed_training.py
│
├── evaluation/
│   ├── evaluate_metrics.py
│   ├── benchmark.py
│   └── compare_models.py
│
├── inference/
│   ├── batch_inference.py
│   └── api_server.py
│
└── utils/
    ├── logger.py
    ├── config.py
    └── helpers.py
```

## Common Scripts

### Data Processing
```bash
python scripts/data_processing/preprocess_text.py \
    --input data/raw/dataset.csv \
    --output data/processed/dataset_processed.csv \
    --lowercase --remove_special_chars
```

### Training
```bash
python scripts/training/train_classifier.py \
    --model bert-base-uncased \
    --train_data data/processed/train.csv \
    --config configs/training_config.yaml \
    --output_dir models/checkpoints/bert-classifier-v1
```

### Evaluation
```bash
python scripts/evaluation/evaluate_metrics.py \
    --predictions model_output.json \
    --ground_truth test_labels.json \
    --metrics accuracy f1 precision recall
```

## Writing Good Scripts

### Template Structure
```python
#!/usr/bin/env python
"""
Script description: What this script does

Usage:
    python script_name.py --arg1 value --arg2 value
"""

import argparse
import logging
from pathlib import Path

# Setup logging
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

def parse_args():
    parser = argparse.ArgumentParser(description=__doc__)
    parser.add_argument("--input", type=Path, required=True)
    parser.add_argument("--output", type=Path, required=True)
    return parser.parse_args()

def main(args):
    logger.info(f"Processing {args.input}")
    # Your code here
    logger.info(f"Output saved to {args.output}")

if __name__ == "__main__":
    args = parse_args()
    main(args)
```

### Best Practices
- Use `argparse` for CLI arguments
- Include docstrings
- Add logging for debugging
- Use type hints
- Handle errors gracefully
- Create config files for hyperparameters
- Test scripts locally first

## Running Scripts

### From Python
```python
import subprocess

result = subprocess.run([
    "python", "scripts/training/train_classifier.py",
    "--model", "bert-base",
    "--epochs", "3"
], capture_output=True, text=True)

print(result.stdout)
```

### In Notebooks
```python
%run scripts/training/train_classifier.py --model bert-base --epochs 3
```

## Script Categories

### 📊 Data Processing
- Loading and parsing different formats
- Text cleaning and normalization
- Tokenization and preprocessing
- Data augmentation techniques
- Train/val/test splitting

### 🎓 Training
- Model initialization
- Training loops
- Distributed training setup
- Checkpoint management
- Learning rate scheduling

### 📈 Evaluation
- Metric calculation (accuracy, F1, BLEU, etc.)
- Comparison across models
- Visualization utilities
- Statistical testing

### 🚀 Inference
- Batch prediction
- API server setup
- Model deployment
- Latency optimization

### 🔧 Utilities
- Configuration loading
- Logging setup
- Result tracking
- Version control

## Configuration Files

Use YAML for configuration:
```yaml
# configs/training_config.yaml
model:
  name: "bert-base-uncased"
  pretrained: true

training:
  learning_rate: 5e-5
  batch_size: 32
  epochs: 3
  warmup_steps: 500

data:
  train_path: "data/processed/train.csv"
  val_path: "data/processed/val.csv"
  test_path: "data/processed/test.csv"

output:
  save_dir: "models/checkpoints/bert-classifier-v1"
  log_dir: "logs"
```

Load in Python:
```python
import yaml

with open("configs/training_config.yaml") as f:
    config = yaml.safe_load(f)

model_name = config["model"]["name"]
batch_size = config["training"]["batch_size"]
```

## Sharing Scripts

- Document expected input/output formats
- Include example usage
- Add error handling
- Write tests when possible
- Version your scripts

## See Also
- [Training Techniques](../concepts/3-training-techniques/)
- [Data Management](../data/)
- [Model Management](../models/)
