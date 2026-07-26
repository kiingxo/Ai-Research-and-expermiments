# Experiment: Hybrid decision authority

**Status:** observed (qualitative; ongoing systems work)
**Theme:** reliability, multi-agent coordination
**Date opened:** 2026-05
**Last updated:** 2026-07-26

## Hypothesis

Agent systems are more reliable when probabilistic model judgment is separated
from deterministic responsibilities (identity, arithmetic, retries, ordering of
hard facts) and a human retains authority over irreversible external actions.

Falsifiable: if the model must invent hard facts or execute irreversible actions
for the loop to function, the split has failed.

## Method

Non-proprietary method only:

1. **Baseline:** loops where model narrative and mechanical conclusions were not
   clearly separated.
2. **Split under test:** model proposes interpretations and alternatives; code
   owns reproducible checks; humans own final external commitment.
3. **Evaluation lens:** can a later reviewer tell which layer produced which
   claim? Did mechanical conclusions ever depend on free-text confidence?
4. **Ambiguity rule:** when observation gaps make order unknowable, store
   ambiguity instead of forcing a winner.

## What Ran

- Applied as a design rule across Blueprint agent systems work in 2026.
- Compared attended demos with continuous operation (authority bugs surface
  faster when nobody is watching).
- No public accuracy metrics are attached to this note.

## Result / Failure

**Held (qualitative)**

- Separating interpretation from reproducible fact made post-mortems clearer.
- Expanding autonomy past an enforceable trust boundary failed and was rolled
  back (principle: end the agent where trust ends).

**Failed earlier**

- Treating model-inferred events as ground truth created silent label errors.
  See [failures/LOG](../../failures/LOG.md).

## Next

- Prospective evals that score decision quality with frozen authority rules.
- Explicit test cases where ambiguity must remain unresolved.
