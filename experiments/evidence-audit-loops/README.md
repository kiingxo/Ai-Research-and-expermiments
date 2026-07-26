# Experiment: Evidence trails and audit loops

**Status:** observed (qualitative)  
**Theme:** auditability, memory, evaluation  
**Date opened:** 2026-06  
**Last updated:** 2026-07-26

## Hypothesis

Multi-agent decision systems stay debuggable only if each decision leaves a
reconstructable trail (inputs role-tagged, model version, deterministic checks,
human action, later outcome, ambiguity flags), and if memory cannot change live
behaviour until evidence and review allow it.

Falsifiable: if a bad decision cannot be reconstructed without chat folklore, or
if one reflection can alter tomorrow’s prompt, the audit loop has failed.

## Method

1. **Baseline:** chat-centric outputs with thin reconstructability.
2. **Trail minimum (principle-level):** what was observed, inferred, checked by
   code, done by a human, and what happened later — plus model/prompt version
   tags when prompts change.
3. **Cohort hygiene:** do not mix incomparable outcome processes into one score.
4. **Memory coupling:** retrieve in shadow first; freeze live injection until
   prospective checks pass (see also [playbook-memory](../playbook-memory/) for
   the memory-specific protocol already in this repo).

## What Ran

- Used evidence-first post-mortems during Blueprint agent work instead of
  prompt-only iteration.
- Shadow-style memory evaluation kept baselines intact while asking whether
  retrieval would have helped.

## Result / Failure

**Held**

- Reconstructability beat another round of instruction polishing for several
  failure classes (stale context, mixed cohorts, inferred-as-fact events).
- Shadow retrieval preserved a baseline.

**Incomplete**

- No verified public performance claim.
- Live memory injection remains gated on evidence criteria, not vibes.

## Next

- Prospective evaluation with frozen versions and published inclusion rules if
  sample quality allows.
- Manual relevance ratings on shadow retrievals before any injection trial.
