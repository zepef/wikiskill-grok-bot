---
name: wikiskill-gate
description: Accept a proposed skill only if held-out score is strictly higher than R_best. Enable only on the Referee Bot. Human approval required to promote.
user-invocable: false
---

# Wiki Gate

Enable only on Referee.

## When to use

After Coach posted a candidate, or on the 03:00 routine.

## Sequence

1. If `bench/val` is empty, post "no validation bench" in Loop and stop.
2. If `skills/proposed/` is empty, post "no candidate" and stop.
3. Score held-out tasks with current skills versus current + candidate.
4. Reject if R_val <= R_best: archive, append skill-impact, do not touch production.
5. Accept if R_val > R_best: wait for human Allow, then save/update and enable on workers only.

Never Always-allow promote.
