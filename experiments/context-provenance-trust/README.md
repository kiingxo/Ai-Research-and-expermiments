# Experiment: Context provenance and trust boundaries

**Status:** observed (iterated)
**Theme:** reliability, multi-agent coordination
**Date opened:** 2026-05
**Last updated:** 2026-07-26

## Hypothesis

Multi-source agent context fails when every input is treated as equal "context."
Reliability improves when each fact carries provenance (source, time, scope,
freshness) and a trust boundary states who may conclude what.

Falsifiable: if stale, missing, or wrong-scope inputs can silently dominate a
decision without an explicit conflict rule, provenance design is insufficient.

## Method

1. **Baseline:** pack more text/images into the prompt and hope ranking emerges.
2. **Required metadata (principle-level):** source, timestamp, scope key, freshness
   state, and role (evidence vs summary vs preference vs inference).
3. **Conflict rule:** newer authoritative observations beat stale summaries for
   mechanical fields; model may discuss conflict but not erase it.
4. **Missing data:** represent absence explicitly; do not let the model invent
   mechanical substitutes.

## What Ran

- Used as a recurring review checklist while building multi-surface agents at
  Blueprint Labs (private systems; internals not documented here).
- Failure cases logged when coherent answers followed bad or stale inputs.

## Result / Failure

**Observed**

- Provenance fields catch a class of confident-wrong answers that prompt edits
  do not.
- Continuity of old context is often mistaken for validity.

**Not claimed**

- No published latency or accuracy deltas.

## Human-facing surfaces (product level)

Provenance is not only for machines reconciling context. Agent systems people
can actually use need **decision provenance for humans**: readable reasons on
calls, session briefings that frame the desk before action, a shared track
record, and a Floor where state is visible instead of buried in logs.

On [Leverage](https://leverage.blueprintlabsai.tech/), those surfaces include:

| Surface | What the human gets (no internals) |
| --- | --- |
| **Decision reasons** | Each call exposes a why you can weigh, challenge, or ignore before you act. |
| **Brief** | Session briefings that answer what matters now at the open, not after price has moved. |
| **Track Record** | A shared weekly board of published calls so outcomes stay inspectable. |
| **Floor** | The hosted desk where agents, calls, and context are visible as a working session. |

**Hypothesis (human leg):** if the only artifact is a label or a push notification,
users treat the system as a black box. If reasons and briefings are first-class
product surfaces, collaboration improves even when the underlying orchestration
stays private.

**Observed (qualitative):** traders ask for the why before they ask for another
scan. Briefings reduce "what did I miss?" at session handoffs. This repo does
not document how those surfaces are built; it records that they matter for trust.

## Next

- Count conflict cases (fresh vs stale) in prospective logs without publishing
  proprietary payloads.
- Tool-use policy: dynamic research tools only when investigation is the task,
  not on every turn.
- Prospective note-taking: when users ignore a call, do they cite missing or
  weak decision reasons (product signal, not prompt archaeology).
