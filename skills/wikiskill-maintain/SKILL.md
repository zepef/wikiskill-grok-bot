---
name: wikiskill-maintain
description: Distill new raw traces into persistent wiki pattern pages. Enable only on the Archivist Bot. Never edit production skills.
user-invocable: false
---

# Wiki Maintainer

Enable only on Archivist. Workers must not have this skill.

## When to use

Nightly routine, or when Loop asks for a wiki pass after a batch of traces.

## Required access

Read `/workspace/wikiskill/raw`
Write `/workspace/wikiskill/wiki`
Read `STATE.md`
No production skill save/update/enable.
No messages to Worker Bots.

## Sequence

1. Read `wiki/log.md` to find the last consumed raw file.
2. List new files under `raw/` since that point. Cap: 20 files.
3. Sample up to 5 failing traces and 3 passing traces.
4. For each recurring failure or working move, create or update one file in `wiki/patterns/`.
5. Update `wiki/index.md` and append `wiki/log.md`.
6. Post a short summary in the Loop group.
7. Stop.

Ground every claim in a named raw file. If you cannot, do not write the pattern.
