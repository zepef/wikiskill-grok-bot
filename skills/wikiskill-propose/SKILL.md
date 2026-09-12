---
name: wikiskill-propose
description: Propose exactly one skill create or patch from the wiki. Enable only on the Coach Bot. Never activate the skill.
user-invocable: false
---

# Skill Proposer

Enable only on Coach.

## When to use

After the Archivist has posted a wiki summary, or on the 02:30 routine.

## Required access

Read `wiki/index.md`, `wiki/skill-impact.md`, `wiki/patterns/`, `STATE.md`
Write only `/workspace/wikiskill/skills/proposed/<name>/`
No wiki edits. No skill enable. No Worker messages.

## Sequence

1. Read skill-impact.md. Do not repeat a rejected change.
2. Pick one gap the wiki documents and production skills do not cover.
3. Write exactly one candidate SKILL.md plus PURPOSE.md.
4. Post the diff in Loop.
5. Stop.

One skill. One change. Nothing enabled.
