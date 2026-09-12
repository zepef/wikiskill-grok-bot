---
name: wikiskill-log-trace
description: Append an immutable execution trace after a finished Grok Bot task. Use at the end of any worker job. Never read the wiki.
user-invocable: true
---

# Log a WikiSkill trace

## When to use

After a Worker Bot finishes a task that used a production skill. Success and failure both get a trace.

## Required access

Write only to `/workspace/wikiskill/raw/YYYY-MM-DD/`.
Do not read `/workspace/wikiskill/wiki`.
Do not read `skill-impact.md`.
Do not read `skills/proposed`.

## Sequence

1. Create the day folder if missing.
2. Write one new file: `<bot>-<task-id>.jsonl`. Never overwrite an existing file.
3. Append one line to `raw/_index.md`: date, bot, task-id, skill used, ok/fail.
4. Stop.

## Sanitize before write

Strip tokens, passwords, message bodies, personal names, account numbers.
Keep tool names, skill names, pass/fail, short error codes.

## Approval

None for an append under `raw/`.
