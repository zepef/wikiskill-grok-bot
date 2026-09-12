# Routines — coller dans le Bot propriétaire, après un test run manuel.

Plafonds produit : 50 routines / Bot, 20 derniers runs visibles.
Les traces vivent donc sur /workspace, pas dans l’historique de routine.

## Archivist — 02:00

Every night at 02:00, timezone of this account, run the wiki-maintainer skill on /workspace/wikiskill.
Read only new files under raw/ since the last log entry.
Update wiki/patterns, wiki/index.md and wiki/log.md.
Sanitize secrets before writing a pattern.
Post a short summary in the Loop group: new patterns, files read, files skipped.
If raw/ has nothing new, post "no new traces" and stop.
Never save or enable a production skill.
Never message a Worker Bot.
If the computer cannot see /workspace/wikiskill, report the failure and stop. Do not invent traces.

## Coach — 02:30

Every night at 02:30, run the skill-proposer skill.
Read wiki/index.md, wiki/skill-impact.md, STATE.md, and at most 5 failing + 3 passing traces named by the Archivist.
Propose exactly one create or one patch.
Write it to /workspace/wikiskill/skills/proposed/<name>/SKILL.md plus PURPOSE.md.
Post the diff in Loop.
Do not activate the skill. Do not edit the wiki.
If skill-impact.md already rejected this change, pick a different change or post "no safe proposal" and stop.

## Referee — 03:00

Every night at 03:00, run the wiki-gate skill.
Score /workspace/wikiskill/bench/val with the proposed skill versus the current enabled skills.
Accept only if R_val > R_best.
On reject: archive the proposal, append skill-impact Rejected, do not touch production skills.
On accept: post scores + diff in Loop and wait for my approval before saving or enabling any skill.
Never Always-allow the promote step.
If bench/val is empty, post "no validation bench" and stop. Do not invent scores.

## Workers — pas de routine evolve

Ajouter seulement ceci dans les skills métier des workers, en fin de tâche :
After finishing, run /wikiskill-log-trace and append one JSONL file under /workspace/wikiskill/raw/YYYY-MM-DD/.
Do not open wiki/, skill-impact.md, or skills/proposed/.
