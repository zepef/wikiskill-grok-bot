# WikiSkill for Grok Bot
<img width="1984" height="992" alt="image" src="https://github.com/user-attachments/assets/1d62aebc-e745-4d81-82c7-7546cbc7bfe5" />


Native adaptation of [WikiSkill](https://arxiv.org/abs/2608.27454) (Google Research, August 27, 2026) on **Grok Bot primitives only**.

No external CLI. No outside harness. No company playbook.

Grok Bot already knows: do a task → save a skill → schedule a routine.

This pack adds the missing loop:

1. keep traces of successes **and** failures
2. compile a persistent wiki that **workers must not read**
3. propose **one** atomic skill change per cycle
4. promote the skill only if a held-out score strictly improves

Paper: Tang et al., *WikiSkill: Compiling Agent Experience into Persistent Knowledge for Skill Evolution*, [arXiv:2608.27454](https://arxiv.org/abs/2608.27454).

X Article (US): [docs/article-x/us.md](docs/article-x/us.md)  
Article X (FR): [docs/article-x/fr.md](docs/article-x/fr.md)

## Why Grok Bot

| WikiSkill (paper) | Grok Bot primitive |
|---|---|
| Inference agent | Your existing worker Bots |
| Raw layer | `/workspace/wikiskill/raw/` (append-only) |
| Wiki layer | `/workspace/wikiskill/wiki/` + Archivist thread |
| Skill layer | Grok Bot Skills, **enabled per Bot** |
| Wiki Maintainer | Bot **Archivist** + nightly routine |
| Skill Proposer | Bot **Coach** + routine |
| Gate | Bot **Referee** + human Allow |
| Isolation | Per-Bot skill enablement + Team Rule + separate group chat |

Hard product constraint: every Bot on an account shares **one** cloud computer (`/workspace`, cookies, connectors). Bots are not a security boundary. Isolation is organizational, not an ACL.

## Roster

Three new Bots. Your workers stay workers.

| Bot | Job | Skills ON | Routine |
|---|---|---|---|
| Your workers | the work | domain skills + `wikiskill-log-trace` + `wikiskill-worker-guard` | yours |
| **Archivist** | compile traces → wiki | `wikiskill-maintain` | 02:00 |
| **Coach** | one create/patch per cycle | `wikiskill-propose` | 02:30 |
| **Referee** | accept only if validation beats best | `wikiskill-gate` | 03:00 |

Group chat **Loop** = Archivist + Coach + Referee + you. In the French article the same room is **la Boucle**.

**No worker Bot in Loop.** They must not watch the wiki being written.

## Install (4 pastes)

1. Paste `prompts/create-bots.md` — creates the three Bots.
2. Paste `prompts/create-group.md` — creates Loop.
3. Send `prompts/init-workspace.md` to Archivist.
4. After one **manual test run**, paste `prompts/create-routines.md` on each owning Bot.

Then: **Settings → Plugins → Yours** and enable skills per the matrix in [`TEAM.us.md`](TEAM.us.md).

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

## License

MIT. The research paper is Google Research / Virginia Tech. This repository is an independent adaptation of the published method to Grok Bot. It is not an xAI or Google product.

Lab X: https://le-lab-x.com
