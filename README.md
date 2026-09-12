# WikiSkill for Grok Bot

[Français](README.fr.md) · [X article (US)](docs/article-x/us.md) · [Article X (FR)](docs/article-x/fr.md)

Native adaptation of [WikiSkill](https://arxiv.org/abs/2608.27454) (Google Research, 27 Aug 2026) on **Grok Bot primitives only**.

No external command line. No outside harness. No company playbook.

Grok Bot already knows how to run a task, save a skill, and schedule a routine. This pack adds the missing loop:

1. Keep traces of successes **and** failures.
2. Compile a persistent wiki that **workers must not read**.
3. Propose **one** skill change per cycle.
4. Promote the skill only if a held-out score strictly improves.

Paper: Tang et al., *WikiSkill: Compiling Agent Experience into Persistent Knowledge for Skill Evolution*, arXiv:2608.27454.

## Why Grok Bot

| WikiSkill (paper) | Grok Bot primitive |
|---|---|
| Inference agent | Your existing worker Bots |
| Raw layer | `/workspace/wikiskill/raw/` (append-only) |
| Wiki layer | `/workspace/wikiskill/wiki/` + Archivist thread |
| Skill layer | Grok Bot Skills, **enabled per Bot** |
| Wiki Maintainer | Bot **Archivist** + nightly routine |
| Skill Proposer | Bot **Coach** + routine |
| Gate | Bot **Referee** + human approval |
| Isolation | Per-Bot skill enablement + Team Rule + separate group chat |

Hard product constraint: every Bot on an account shares **one** cloud computer (`/workspace`, connectors). Bots are not a security boundary. Isolation is organizational, not a file ACL.

## Roster

Three new Bots. Your workers stay workers.

| Bot | Job | Skills ON | Routine |
|---|---|---|---|
| Your workers | the work | domain skills + `wikiskill-log-trace` + `wikiskill-worker-guard` | yours |
| **Archivist** | traces → wiki | `wikiskill-maintain` | 02:00 |
| **Coach** | one create or patch per cycle | `wikiskill-propose` | 02:30 |
| **Referee** | accept only if validation score beats the current best | `wikiskill-gate` | 03:00 |

Group chat **Loop** = Archivist + Coach + Referee + you.

**No worker Bot in Loop.** They must not watch the wiki being written.

## Install (four pastes)

1. Paste [`prompts/create-bots.md`](prompts/create-bots.md).
2. Paste [`prompts/create-group.md`](prompts/create-group.md).
3. Send [`prompts/init-workspace.md`](prompts/init-workspace.md) to Archivist.
4. After one **manual test run**, paste [`prompts/create-routines.md`](prompts/create-routines.md) on each owning Bot.

Then: **Settings → Plugins → Yours** and enable skills per the matrix in [`TEAM.md`](TEAM.md) / [`TEAM.en.md`](TEAM.en.md).

Do not start the nightly routines before `/workspace/wikiskill/bench/val` contains held-out tasks and a grader. Without that, Referee must stop.

## Layout on the shared computer

```
/workspace/wikiskill/
  raw/YYYY-MM-DD/<bot>-<task>.jsonl
  wiki/{index,log,skill-impact,patterns}/
  skills/{active,proposed,archive}/
  bench/{train,val,graders}/
  STATE.md
```

Production skills do **not** live here. They live in Grok Bot → Settings → Plugins → Yours.

`/workspace` holds evidence, wiki, and staging. After ACCEPT + human Allow: native *Save/update skill*, then enable on worker Bots only.

## Skills in this repo

| Skill | Enable on | Invocable |
|---|---|---|
| [`wikiskill-log-trace`](skills/wikiskill-log-trace/SKILL.md) | Workers | yes |
| [`wikiskill-worker-guard`](skills/wikiskill-worker-guard/SKILL.md) | Workers | no |
| [`wikiskill-maintain`](skills/wikiskill-maintain/SKILL.md) | Archivist only | no |
| [`wikiskill-propose`](skills/wikiskill-propose/SKILL.md) | Coach only | no |
| [`wikiskill-gate`](skills/wikiskill-gate/SKILL.md) | Referee only | no |

## Product limits

- 50 routines per Bot, 20 stored runs each — traces must live on disk
- Group chat: 2–6 Bots
- Connectors are account-wide
- Teach a task ≤ 10 minutes — use it to **seed** a skill, not to run the loop
- Approvals do not undo completed work

## Anti-patterns

- Enabling `wikiskill-maintain` on a worker “so it improves by itself” (paper ablation: the actor reading the wiki **hurts** the skill)
- Putting a worker in Loop
- Treating the 20 routine records as the raw layer
- Letting Coach enable the candidate
- One Bot doing worker + archivist + coach
- Starting routines with an empty `bench/val`

## What this is not

Not a Google CLI. Not an outside harness. Not Drive-as-a-brain. Not a Google Cloud API.

Connectors (Drive, Gmail, Calendar, …) are optional I/O for **workers**. They sit outside the evolution loop.

## License

MIT. The research paper is Google Research / Virginia Tech. This repository is an independent adaptation of the published method to Grok Bot. It is not an xAI or Google product.
