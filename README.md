# AI Research and Experiments

I started this repository while I was learning how language models work. The
older folders contain my notes on transformers, NLP, fine tuning, local models,
and LangGraph. I still keep them because they show the foundation, but they no
longer represent most of my work.

Over the last few months I have been building complete agent systems at
[Blueprint Labs](https://blueprintlabsai.tech). That work changed the questions
I care about. I am now less interested in making a model produce one impressive
answer and more interested in what happens when a model has to work continuously
with live data, tools, state, users, failures, and measurable outcomes.

This repository is where I document that engineering and research process. The
main product code lives in separate repositories. What belongs here is the
reasoning behind the systems, the experiments that shaped them, and the lessons
I do not want to lose.

## What I Am Building

| Project | What I am investigating | Status |
| --- | --- | --- |
| [Leverage](./projects/leverage/) ([Floor](https://leverage.blueprintlabsai.tech/)) | Multimodal market reasoning, decision support, agent evaluation, and memory | Private beta |
| [Apex AI](./projects/apex-ai/) | Real time event processing, fast decision pipelines, and deterministic risk controls | Active production research |
| [Playbook Memory](./experiments/playbook-memory/) | Persistent agent knowledge that cannot promote itself without evidence | Shadow evaluation |
| [Production Agent Systems](./concepts/5-agent-systems/) | Context, tools, state, guardrails, observability, and human control | Ongoing notes |

## Lab Experiments

If you are checking whether multi-agent, memory, and decision-system claims are
backed by work that actually ran, start here — not in manifesto prose.

| Experiment | Theme | Status |
| --- | --- | --- |
| [Hybrid decision authority](./experiments/hybrid-decision-authority/) | Reliability / coordination | Observed (qualitative) |
| [Context provenance trust](./experiments/context-provenance-trust/) | Provenance / trust boundaries | Observed (iterated) |
| [Unattended agent reliability](./experiments/unattended-agent-reliability/) | Ops reliability | Observed (ongoing) |
| [Evidence audit loops](./experiments/evidence-audit-loops/) | Auditability / memory gating | Observed (qualitative) |
| [Playbook Memory](./experiments/playbook-memory/) | Shadow memory promotion | Shadow evaluation |

Failure shapes: [`failures/LOG.md`](./failures/LOG.md). Framing only:
[`notes/`](./notes/). Methods stay principle-level; product internals are out of
scope for this public lab notebook.

## Leverage

Leverage is the system I have spent most of my recent time on. It started as a
Chrome extension that could send a TradingView screenshot to a model. It now has
several distinct workflows:

* **Pulse** scans a selected chart periodically and looks for setups.
* **Co-Pilot** is a chart aware workspace where a trader can discuss a plan,
  challenge the analysis, and ask the system to inspect new chart development.
* **Market Map** keeps Daily and 4H structure separate from the execution chart.
* **Execution Desk** provides an optional second opinion on an existing setup.
* **Trade Monitor** follows a trade after entry and combines objective price
  events with model based management.
* **The Floor** makes the system visible through a live operational interface.

Leverage also includes Telegram delivery, news and calendar context, journals,
P&L cards, paper setup tracking, chart evidence, outcome diagnostics, and a
learning system that currently runs without changing live prompts.

The difficult work has not been adding more instructions to the model. It has
been deciding which source is authoritative, proving whether a target was
actually reached, keeping old chart candles from becoming new events, separating
paper outcomes from trades a user took, and preserving enough evidence to debug
a bad call later.

Public Floor: [leverage.blueprintlabsai.tech](https://leverage.blueprintlabsai.tech/)

[Read the Leverage engineering dossier](./projects/leverage/)

## Apex AI

Apex AI came before Leverage. It observes fast Solana migration markets and
builds state from live events before making a decision. It uses stream
processing, deterministic filters, asynchronous inspection, Telegram delivery,
and post call outcome tracking.

Apex taught me an important systems lesson: the slow intelligence cannot block
the hot path. Event collection and hard validation have to keep moving while AI
inspection, enrichment, and external delivery happen around them.

[Read the Apex AI engineering dossier](./projects/apex-ai/)

## The Questions Behind the Work

### How should an agent see?

Leverage receives chart images, structured prices, market maps, news, economic
events, session state, and prior analysis. More context is not automatically
better. Every source needs an asset, timestamp, freshness state, and clear role.

### What should the model control?

The model can interpret structure, compare explanations, and suggest a plan. It
should not own authentication, TP and SL detection, risk arithmetic, event
idempotency, user permissions, or database integrity. Those need reproducible
answers.

### How do I know whether an agent is improving?

A good explanation is not the same as a good decision. The systems now record
analysis episodes, prompt and model versions, paper and taken cohorts, trade
events, ambiguous outcomes, realized R, MFE, MAE, and later results.

### Can an agent learn without fine tuning?

Playbook Memory tests whether completed episodes can become reusable knowledge.
The important part is not generating lessons. It is controlling evidence,
contradictions, scope, permissions, versioning, and promotion. Retrieval remains
in shadow mode until it proves useful prospectively.

### What does useful collaboration look like?

Pulse is designed for automation. Co-Pilot is designed for discussion. A trader
should be able to disagree, point at a drawing, correct the model, or ignore a
plan. The interface is part of that relationship, not decoration around the
model.

## Engineering Principles I Keep Returning To

### Mechanical truth stays in code

The current chart can inform a decision, but a trusted post entry event should
decide whether TP or SL was crossed. The same rule applies to identity,
permissions, retries, and risk calculations.

### Paper and taken trades are different datasets

A setup may work even when nobody takes it. A user may also close a trade
differently from the published plan. Combining both into one win rate makes the
result difficult to interpret.

### Ambiguity is a valid result

If a polling gap could have crossed both stop and target, I would rather store
`ambiguous` than invent the order of events. Ambiguous cases are excluded from
learning.

### Memory should earn influence

One trade can propose a candidate lesson. It cannot activate that lesson. A
market rule needs repeated evidence, contradiction checks, and human approval
before it can affect another analysis.

### APIs and MCP solve different problems

Direct integrations are better for predictable ingestion and mechanical work.
Model selected tools make sense when dynamic investigation is useful. MCP may
eventually help Co-Pilot search for missing news or retrieve specialised
context, but it is not a replacement for the existing backend.

## Repository Structure

```text
.
├── experiments/          # hypothesis → method → what ran → result (start here)
├── failures/             # dated failure shapes (no internals)
├── notes/                # framing only
├── results/              # outcome pointers (no fake scoreboards)
├── projects/
│   ├── leverage/         # dossier + public Floor link
│   ├── apex-ai/
│   └── earlier fine tuning notebooks
├── concepts/             # foundations learning path
├── data/
├── models/
└── scripts/
```

## Learning Path

The original material is still available in order:

1. [LLM fundamentals](./concepts/1-llm-fundamentals/)
2. [NLP fundamentals and data APIs](./concepts/2-nlp-fundamentals/)
3. [Fine tuning and training techniques](./concepts/3-training-techniques/)
4. [Frameworks and local inference](./concepts/4-frameworks/)
5. [Production agent systems](./concepts/5-agent-systems/)

## Current Direction

The next stage of the work is mostly about measurement:

* Collect clean prospective data for Pulse and Co-Pilot.
* Measure setup performance by asset, setup family, regime, and prompt version.
* Finish evaluating shadow memory before any live injection.
* Explore read only tools for selective news and market research.
* Build Leverage Live as a public view of paper activity without exposing
  private user data.
* Investigate specialised model evaluation and eventual fine tuning without
  treating user behaviour as ground truth.

## Status and Scope

This is an active research repository. Some systems are deployed, some are in
private beta, and some deliberately run in shadow mode. Trading related work is
experimental decision support research. It is not financial advice, and I do
not treat historical outcomes as a promise of future performance.

I want this repository to preserve the real process. That includes good ideas,
bad assumptions, implementation mistakes, and the changes that followed them.
