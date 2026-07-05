# Experiments

This directory contains work that is testing a research question but is not yet
trusted as production behaviour.

## Current Experiments

### [Playbook Memory](./playbook-memory/)

Can an agent build reusable knowledge from its own episodes without immediately
feeding unverified lessons back into future decisions?

The system captures episodes, outcomes, candidates, evidence, and retrievals.
Everything currently runs in shadow mode: retrieval is logged and evaluated but
cannot alter prompts.

### Dawid-Skene Label Aggregation

- [Notebook](./Dawid-Skene-algorithm.ipynb)
- Investigation of latent true labels from multiple noisy annotators.
- Relevant to a recurring problem in agent evaluation: neither users nor models
  should automatically be treated as perfect ground truth.

## Experiment Lifecycle

```text
hypothesis -> instrumentation -> baseline -> prospective run
           -> analysis -> contradiction check -> decision
```

An experiment should document:

1. The claim being tested.
2. A baseline that does not contain the new behaviour.
3. Data inclusion and exclusion rules.
4. Ambiguous or missing observations.
5. Negative results and contradictions.
6. The evidence required before promotion.

## What Does Not Count as Evidence

- A single successful example.
- A persuasive model explanation.
- Retrospectively moving levels after an outcome.
- Combining paper calls with trades a user actually took.
- Treating missing outcomes as wins.
- Repeatedly changing the strategy against the same evaluation sample.

Failed experiments stay documented. Their purpose is to prevent the same idea
from returning later with a different name and no additional evidence.
