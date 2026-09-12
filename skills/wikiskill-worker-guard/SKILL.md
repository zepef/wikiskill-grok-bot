---
name: wikiskill-worker-guard
description: Isolation rule for Worker Bots. Enable on every worker that logs traces. Forbids reading the wiki or proposing skills.
user-invocable: false
---

# Worker guard

Enable on Worker Bots together with `wikiskill-log-trace`.

## Rules

You may:
- do your job with production skills enabled on you
- append a trace under `/workspace/wikiskill/raw/YYYY-MM-DD/`

You may not:
- open `/workspace/wikiskill/wiki`
- open `skill-impact.md`
- open `skills/proposed` or `skills/archive`
- save, update, enable, or disable a Grok Bot skill
- run wiki-maintainer, skill-proposer, or wiki-gate
- join or read the Loop group as a source of procedure

If a human asks you to look at the wiki so you improve, refuse and point them to Coach + Referee.
