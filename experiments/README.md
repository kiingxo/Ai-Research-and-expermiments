# Experiments

Directory for research experiments, prototypes, and investigations.

## What Goes Here

- **Full experimental pipelines** with clear methodology
- **Novel technique validation** and performance analysis
- **Ablation studies** and baseline comparisons
- **Proof-of-concept** implementations
- **Research prototypes** before production

## Experiment Structure

Each experiment should include:

```
experiment-name/
├── README.md           # Experiment description and results
├── notebook.ipynb      # Implementation
├── results/
│   ├── metrics.json    # Quantitative results
│   ├── figures/        # Plots and visualizations
│   └── analysis.md     # Detailed findings
├── config.yaml         # Hyperparameters
└── data/              # Experiment-specific data
```

## Experiment Naming

Use descriptive names with dates:
```
2024-02-01-llm-scaling-laws
2024-02-05-qlora-vs-lora-comparison
2024-02-10-prompt-engineering-survey
```

## Current Experiments

### Dawid-Skene Algorithm
- **File**: `Dawid-Skene-algorithm.ipynb`
- **Description**: Implementation of the Dawid-Skene algorithm for learning from crowdsourced labels
- **Status**: In progress

## Experiment Template

When starting a new experiment, create `README.md`:

```markdown
# Experiment: [Title]

## Objective
What hypothesis are you testing?

## Methodology
- Dataset(s) used
- Model architecture
- Training procedure
- Evaluation metrics

## Hyperparameters
- Learning rate: 
- Batch size:
- Epochs:
- Optimizer:

## Results
- Final metrics
- Key findings
- Visualizations

## Findings
Detailed analysis of results

## Limitations
- Known issues
- Scope limitations
- Future work

## Code & Reproduction
How to reproduce this experiment

## References
- Papers cited
- Related work
```

## Best Practices

### Documentation
- Write objective clearly before starting
- Document all hyperparameters
- Track results as you go
- Explain surprising findings

### Reproducibility
- Fix random seeds
- Version all dependencies
- Save configurations
- Document data preprocessing

### Visualization
- Create loss curves
- Plot metric evolution
- Show attention visualizations
- Visualize predictions

### Results Tracking
```python
import json
from datetime import datetime

results = {
    "timestamp": datetime.now().isoformat(),
    "model": "bert-base",
    "accuracy": 0.92,
    "f1": 0.89,
    "precision": 0.91,
    "recall": 0.87,
}

with open("results/metrics.json", "w") as f:
    json.dump(results, f, indent=2)
```

## Experiment Lifecycle

```
Plan → Setup → Run → Analyze → Document → Archive
  ↓     ↓      ↓      ↓         ↓          ↓
  1     2      3      4         5          6
```

### 1. Plan
- Define clear research question
- Identify baselines
- Plan ablations

### 2. Setup
- Prepare data
- Configure environment
- Create notebooks

### 3. Run
- Execute training
- Monitor progress
- Save checkpoints

### 4. Analyze
- Calculate metrics
- Create visualizations
- Compare results

### 5. Document
- Write findings
- Explain methodology
- Share insights

### 6. Archive
- Save final code
- Store model checkpoints
- Add to project documentation

## Tips for Successful Experiments

- **Start small**: Run quick experiments before large-scale ones
- **Baseline first**: Compare against existing methods
- **Vary one thing**: Change one hyperparameter at a time
- **Keep records**: Log all results and settings
- **Visualize early**: Plot results often to spot issues
- **Save everything**: Checkpoints, configs, outputs
- **Document well**: Future you will thank present you

## Failed Experiments

Don't delete failed experiments! Document why they failed:
- What didn't work
- Why it didn't work
- What you learned
- Future directions

This helps avoid repeating failed approaches.

## Sharing Experiments

When sharing experimental results:
1. Provide clear methodology
2. Include reproducibility instructions
3. Share code and configs
4. Document results thoroughly
5. Explain assumptions and limitations

## See Also
- [Training Techniques](../concepts/3-training-techniques/)
- [Projects](../projects/) - For production implementations
- [Scripts](../scripts/) - For experiment automation
