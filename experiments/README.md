# Experiments

Work that tests a research question. Prefer these writeups over manifesto prose
when checking whether multi-agent, memory, or decision-system claims are backed
by something that actually ran.

Public product surfaces may be linked elsewhere in this repo. Experiment methods
here stay non-proprietary: principles, eval design, and failure shapes only.

## Experiment registry

| Experiment | Hypothesis (short) | Status |
| --- | --- | --- |
| [Hybrid decision authority](./hybrid-decision-authority/) | Separate model judgment from deterministic facts and human commitment | Observed (qualitative) |
| [Context provenance trust](./context-provenance-trust/) | Provenance + trust boundaries beat dumping more context | Observed (iterated) |
| [Deliberation before commitment](./deliberation-before-commitment/) | Reason-first posture beats opaque instant action at the desk | Observed (qualitative) |
| [Unattended agent reliability](./unattended-agent-reliability/) | Unattended loops fail quietly unless darkness is observable | Observed (ongoing) |
| [Evidence audit loops](./evidence-audit-loops/) | Reconstructable trails + gated memory keep systems debuggable | Observed (qualitative) |
| [Playbook Memory](./playbook-memory/) | Episodic lessons must not self-promote into live prompts | Shadow evaluation |
| [Dawid-Skene notebook](./Dawid-Skene-algorithm.ipynb) | Aggregate noisy labels without treating one annotator as truth | Notebook investigation |

## Lab conventions

Copy [`TEMPLATE.md`](./TEMPLATE.md) for new work.

Required sections:

1. Hypothesis (falsifiable)
2. Method (baseline, measurement rules, inclusion, ambiguity) — no internals
3. What ran (honest environment — notebook / shadow / beta)
4. Result / failure (no invented metrics)
5. Next (falsifiable follow-up)

Related folders:

- [`../failures/`](../failures/) — dated failure log (shapes only)
- [`../results/`](../results/) — pointers to outcomes (no fake scoreboards)
- [`../notes/`](../notes/) — framing only, labeled as such
- [`../projects/`](../projects/) — product dossiers / public links

## Lifecycle

```text
hypothesis -> instrumentation -> baseline -> prospective run
           -> analysis -> contradiction check -> decision
```

## What Does Not Count as Evidence

- A single successful example.
- A persuasive model explanation.
- Retrospectively editing labels after an outcome.
- Mixing incomparable outcome cohorts into one score.
- Treating missing outcomes as wins.
- Repeatedly changing the strategy against the same evaluation sample.
- Conceptual essays without a "what ran" section.

Failed experiments stay documented. Their purpose is to prevent the same idea
from returning later with a different name and no additional evidence.
