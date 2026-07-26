# Failure log

Principle-level failures from building continuous agent systems at Blueprint
Labs (2026). Dates are approximate phases, not a controlled trial. This log
records failure *shapes* — not product internals.

---

## 2026-05 — Coherent answer, wrong observation

**Related:** [context-provenance-trust](../experiments/context-provenance-trust/)

**Observed:** Model output looked sensible while the underlying observation was
wrong-scope or stale. Downstream reasoning inherited bad evidence.

**Failure shape:** eloquence ≠ correct inputs.

**Change that followed:** Require provenance and freshness before trusting an
analysis path.

---

## 2026-05/06 — Inference treated as mechanical fact

**Related:** [hybrid-decision-authority](../experiments/hybrid-decision-authority/)

**Observed:** Free-text or visual inference was used to assert events that needed
a reproducible checker. Labels drifted; post-mortems argued with ghosts.

**Failure shape:** probabilistic judgment impersonating hard truth.

**Change that followed:** Keep mechanical conclusions in deterministic code;
allow models to advise, not mint those facts.

---

## 2026-06 — Incomparable outcomes averaged together

**Related:** [evidence-audit-loops](../experiments/evidence-audit-loops/)

**Observed:** Mixing different decision processes into one score made results
uninterpretable.

**Failure shape:** cohort collapse.

**Change that followed:** Separate cohorts; exclude ambiguous cases from
promotion into learning.

---

## 2026-06 — Old context kept authority by inertia

**Related:** [context-provenance-trust](../experiments/context-provenance-trust/)

**Observed:** Continuity of an older summary felt like expertise. It was expiry
failure.

**Failure shape:** continuity mistaken for validity.

**Change that followed:** Explicit freshness/missing states in context assembly.

---

## 2026-06/07 — Unattended loops failed quietly

**Related:** [unattended-agent-reliability](../experiments/unattended-agent-reliability/)

**Observed:** Background work stalled without a user-visible fault. Discovery
came from absence of useful output.

**Failure shape:** silence as an unmarked symptom.

**Change that followed:** Shared operational visibility for agent/job liveness.

---

## 2026-07 — Presence mistaken for authorization

**Related:** [unattended-agent-reliability](../experiments/unattended-agent-reliability/)

**Observed:** A surface still looked "on" after trust had expired, producing mute
or partial behaviour blamed on the model.

**Failure shape:** UI presence ≠ authorization.

**Change that followed:** Treat auth/session validity as a continuous signal in
ops review (implementation stays private).

---

## 2026-07 — Autonomy past the trust boundary

**Related:** [hybrid-decision-authority](../experiments/hybrid-decision-authority/)

**Observed:** Automating an irreversible external action looked like completion
until trust could not be enforced.

**Failure shape:** autonomy expanded past accountability.

**Change that followed:** Keep humans on irreversible commitments; agents
observe, propose, monitor, and record.
