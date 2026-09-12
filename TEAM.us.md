# WikiSkill Desk — Grok Bot roster

[Français](TEAM.md)

Three specialized Bots. Your workers stay workers.
Create a fourth Bot only if you do not have a worker yet.

Product limit: 2–6 Bots per group chat. This desk uses 3.

## Roster

| Bot | Job | Enable | Do not enable | Routine |
|---|---|---|---|---|
| **Archivist** | Compile traces into the wiki. Never does domain work. | `wikiskill-maintain` | domain skills, write connectors | 02:00 |
| **Coach** | Propose **one** skill patch per cycle. Does not edit the wiki. | `wikiskill-propose` | domain skills, `wikiskill-maintain` | 02:30 |
| **Referee** | Run the held-out set. Accept or roll back. | `wikiskill-gate` | write-domain skills | 03:00 |
| Your workers | Do the work. Read active skills only. | domain skills + `wikiskill-log-trace` + `wikiskill-worker-guard` | `wikiskill-maintain`, `wikiskill-propose`, `wikiskill-gate` | yours |

## Team Rule to paste (Teams / Enterprise)

```
WikiSkill isolation
- Worker Bots must never open /workspace/wikiskill/wiki or skill-impact.md.
- Worker Bots may append traces under /workspace/wikiskill/raw/ only.
- Only Archivist may edit /workspace/wikiskill/wiki.
- Only Coach may write /workspace/wikiskill/skills/proposed.
- Only Referee may promote a proposed skill, and only after a validation
  score strictly higher than the current best, plus human approval.
- Never promote a skill that grants send, purchase, delete, or production
  writes without approval_required: true.
- Connectors are account-wide: do not treat Bot roles as a security boundary.
```
