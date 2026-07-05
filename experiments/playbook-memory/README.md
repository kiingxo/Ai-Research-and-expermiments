# Experiment: Leverage Playbook Memory

## Objective

Test whether Leverage can develop reusable knowledge from completed analyses,
trades, and sessions without fine-tuning the underlying language model and
without allowing one persuasive reflection to contaminate future decisions.

## Hypothesis

An evidence-backed memory layer may improve consistency and reasoning if:

- Episodes and outcomes are captured correctly.
- Paper and user-taken trades remain separate.
- Candidate lessons are not treated as active skills.
- Retrieval is scoped to the asset, workflow, setup, regime, and user.
- Contradictory evidence can suspend a skill.
- Live state always overrides historical memory.

## Architecture

```mermaid
flowchart LR
    ANALYSIS[Analysis episode] --> CASE[Trade or session case]
    CASE --> OUTCOME[Resolved outcome]
    OUTCOME --> CANDIDATE[Candidate lesson]
    CANDIDATE --> EVIDENCE[Support and contradiction]
    EVIDENCE --> REVIEW[Human review]
    REVIEW --> SKILL[Versioned skill]
    SKILL --> RETRIEVAL[Shadow retrieval]
    RETRIEVAL --> EVAL[Later outcome evaluation]
```

## Persistence Model

SQLite is authoritative. Markdown may be exported for humans, but free-form
files are not trusted as the canonical memory store.

The system records:

- Authenticated clients and roles.
- Immutable analysis episodes.
- Canonical trade cases and idempotent events.
- Chart-artifact references.
- Candidate lessons and evidence links.
- Versioned global and personal skills.
- Retrieval runs, conflicts, and manual relevance ratings.
- Prompt, model, and context versions.

## Safety Policy

- A single trade may create a candidate but can never activate it.
- Global inferred skills require owner approval.
- Personal behaviour remains private to the user.
- Historical imports carry reduced evidence weight.
- Ambiguous outcomes are excluded.
- Contradiction and negative recent expectancy can move a skill back to
  `review_required`.
- At most five skills may match one analysis.
- Competing skills with similar scores are both withheld.
- Mechanical TP/SL and risk guards cannot be changed by memory.

## Implementation Phases

1. Identity and SQLite migrations.
2. Authenticated episode capture.
3. Trade lifecycle and outcome correctness.
4. Shadow retrieval and retrieval-run logging.
5. Asynchronous candidate extraction.
6. Floor Learning review and diagnostics.
7. Shadow evaluation against later outcomes.

All seven collection and evaluation phases are implemented. Live injection is
explicitly frozen.

## Current Evaluation State

`LEVERAGE_MEMORY_INJECTION_ENABLED` remains false by default.

The current operator work is to collect clean new-schema BTC Pulse data and
review:

- Episode capture rate.
- Resolved-trade linkage.
- Paper and taken expectancy separately.
- Ambiguous cases.
- Retrieval relevance ratings.
- Contradictory evidence.
- Stale and review-required skills.

## Activation Criteria

Memory should not enter a live prompt until:

- Analysis capture is at least 95%.
- Resolved-trade linkage is at least 90%.
- There is no cross-user data leakage.
- Shadow mode produces zero prompt differences.
- At least 50 retrievals have been manually reviewed.
- At least 80% of reviewed retrievals are relevant.
- Prospective paper evaluation shows no regression against the no-memory
  baseline.

The first possible rollout would be approved BTC Pulse entry skills only. Every
later workflow would require a separate prospective evaluation.

## Why Shadow Mode Matters

Without shadow mode, every new memory changes the system that is generating the
next sample. That makes it difficult to know whether performance changed because
of the lesson, the market regime, a prompt edit, or random variation.

Shadow retrieval preserves the baseline while still answering the first
question: did the system retrieve something relevant, and would it have helped
or hurt?

## Open Questions

- How much evidence is enough for asset-specific market knowledge?
- Should evidence decay at the same rate across setup types?
- Can deterministic features identify contradictions better than model review?
- When do embeddings add value beyond structured filters and full-text search?
- How should skills transfer between BTC, gold, and index workflows?
