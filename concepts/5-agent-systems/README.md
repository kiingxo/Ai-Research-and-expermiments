# 5. Production Agent Systems

This section captures what changed when I moved from experimenting with models
to building systems that use models continuously.

An agent is not made reliable by a longer prompt. It is a boundary between a
model, tools, state, deterministic software, external systems, and a human.

## A Practical Agent Stack

```text
interface
  -> authenticated request
  -> current observations
  -> structured context
  -> model reasoning
  -> deterministic validation
  -> action or recommendation
  -> event log
  -> later outcome
  -> evaluation
```

Every arrow is a possible failure point. Model quality cannot compensate for a
wrong asset, stale chart, duplicated event, missing timestamp, or misleading
outcome label.

## Model Work Versus Software Work

### Good model responsibilities

- Interpreting visual structure.
- Comparing competing explanations.
- Explaining uncertainty.
- Identifying relevant context.
- Suggesting a plan or asking for missing evidence.
- Summarising a completed session.

### Good deterministic responsibilities

- Authentication and user identity.
- Permissions and approval boundaries.
- Price parsing and risk calculations.
- TP/SL event detection.
- Idempotency and retries.
- Data freshness and asset matching.
- Database constraints and retention.
- Promotion thresholds for learned skills.

The distinction is not that code is always smarter. It is that some facts must
have one reproducible answer.

## Context Engineering

Useful context is selected, attributed, and time-aware.

A production context object should answer:

- Where did this fact come from?
- When was it observed?
- Which asset and timeframe does it describe?
- Is it current, stale, missing, or contradictory?
- Is it evidence, a summary, a user preference, or a model inference?

Passing everything is not context engineering. It is often a way to hide that
the system has not decided what matters.

## APIs, Function Tools, and MCP

MCP is not a replacement for APIs. An MCP server commonly wraps existing APIs
and presents them as model-discoverable tools.

Use direct backend calls when timing and behaviour must be deterministic. Use a
model-selected tool when dynamic investigation is the point of the task.

For Leverage, live price ingestion, lifecycle events, calendar polling, and
notifications remain direct integrations. Read-only news investigation, market
research, and playbook lookup are candidates for MCP because Co-Pilot may need
them selectively rather than on every turn.

## Multimodal State

Images should be retained as evidence, but structured observations should carry
the durable state.

For a chart-reading agent:

- The image shows geometry and context that a parser may miss.
- Structured levels make calculations reproducible.
- Timestamps prevent historical candles from becoming new events.
- A sequence of selected images can show development.
- Saving every image forever is unnecessary; retention and evidence selection
  are part of the design.

## Persistent Memory

Agent memory has at least four distinct forms:

1. **Working state**: what is happening in the current task.
2. **Episode history**: what the agent observed and answered.
3. **User memory**: preferences and personal behaviour.
4. **Playbook knowledge**: reusable claims supported by evidence.

These should not be stored or trusted in the same way. A user's risk preference
can be personal. A market claim needs broader evidence. A single model
reflection should never silently become global truth.

## Evaluation

Agent evaluation must follow the workflow beyond the response:

- Was the correct context available?
- Did the agent use it?
- Was the recommendation internally consistent?
- Did deterministic guards intervene?
- What happened later?
- Was the observation ambiguous?
- Did the user follow the original plan?
- Would a retrieved memory have helped or hurt?

The most useful metric is often not answer quality alone but decision quality
under realistic state, latency, and tool failures.

## Failures That Changed My Approach

- A model confidently attributed a market move to the wrong headline because
  the relevant news was absent.
- Historical chart wicks were mistaken for post-entry TP/SL events.
- A summary of an old image was not equivalent to seeing the chart develop.
- Confidence labels looked precise without being calibrated.
- User outcomes and paper outcomes were mixed, producing misleading analysis.
- Repeated prompt edits made it difficult to compare behaviour across versions.

Each failure moved responsibility away from vague instructions and toward
better instrumentation, state, contracts, or deterministic code.

## Next Questions

- Can selective tool use improve research without damaging latency?
- How many chart frames are enough to represent development?
- Which setup features generalise across assets, and which are asset-specific?
- Can shadow memory retrieval predict better decisions prospectively?
- What evidence is sufficient before an inferred skill enters a live prompt?
