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

## Next

- Count conflict cases (fresh vs stale) in prospective logs without publishing
  proprietary payloads.
- Tool-use policy: dynamic research tools only when investigation is the task,
  not on every turn.
