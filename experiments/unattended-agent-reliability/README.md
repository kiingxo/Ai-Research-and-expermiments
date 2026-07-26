# Experiment: Unattended agent reliability

**Status:** observed (ongoing)
**Theme:** reliability, evaluation
**Date opened:** 2026-06
**Last updated:** 2026-07-26

## Hypothesis

Agent demos under human attention understate failure. Unattended loops fail
through silent stalls, expired trust, and armed state that outlives its
validity. Making "darkness" observable reduces time-to-detect.

Falsifiable: if the only discovery path for a dead loop is "nothing useful
happened," ops visibility is inadequate.

## Method

1. **Baseline:** background agents with logs only operators never open during
   normal use.
2. **Stress:** keep loops running without a babysitter.
3. **Watch for (qualitative):**
   - jobs that stop progressing without a user-visible fault
   - UI presence after authorization has expired
   - goals/candidates that remain armed after expiry
   - delivery path health decoupled from model health
4. **Disclosure:** record failure shapes publicly; keep credentials, prompts,
   and infrastructure private.

## What Ran

- Continuous private operation of Blueprint agent systems during 2026 beta
  phases.
- Post-incident reviews focused on detection latency, not model eloquence.

## Result / Failure

| Mode | Symptom | Direction of fix |
| --- | --- | --- |
| Quiet stall | Work stops; UI still looks calm | Shared ops visibility |
| Trust drift | Surface looks live; actions are unauthorized/mute | Continuous auth as a signal |
| Stale armed state | Old goal still steers behaviour | Explicit expiry |
| Path decoupling | Model OK / delivery dead (or reverse) | Health per path |

No uptime SLOs or incident IDs are published here.

## Next

- Operator triage checklist experiment: identity → observation freshness →
  loop liveness → delivery.
- Treat missing observation as a first-class user-visible state when safe.
