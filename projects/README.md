# Projects

This directory documents systems that moved beyond isolated notebooks into
end-to-end products or sustained engineering research.

## Active Systems

### [Leverage](./leverage/)

A multimodal, browser-native market decision workstation combining live chart
images, structured market context, deterministic trade tracking, human-in-the-
loop analysis, and shadow-mode agent learning.

**Status:** active private beta and evaluation.

### [Apex AI](./apex-ai/)

A real-time event agent for Solana migration markets, built around streaming
state, deterministic decision gates, asynchronous AI inspection, alerts, and
post-call measurement.

**Status:** active production research.

## Earlier Model Experiments

### ASCII Art Completion Fine Tuning

- [Notebook](./ascii_art_completion_finetuning.ipynb)
- Fine-tuning experiment for structured creative completion.
- Important as an early exercise in dataset construction and specialised model
  behaviour.

### Paul Graham Conversational Fine Tuning

- [Notebook](./conversation_finetuning_paul_graham.ipynb)
- Experiment in turning a bounded essay corpus into conversational training
  examples.
- Raised early questions about imitation, source quality, and whether
  fine-tuning is necessary when retrieval may be more appropriate.

## Documentation Standard

Every substantial project dossier should state:

- The problem and research question.
- The system boundary and architecture.
- What is model-driven and what is deterministic.
- The data and evaluation method.
- Known failures and limitations.
- Current maturity: experiment, shadow, beta, or deployed.
- The next falsifiable question, not only a feature wish list.
