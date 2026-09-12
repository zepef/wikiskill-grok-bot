# Send to Archivist once / Envoyer à Archivist (une fois)

Initialize /workspace/wikiskill if it does not exist.

Create this tree and nothing else:

/workspace/wikiskill/README.md
/workspace/wikiskill/STATE.md
/workspace/wikiskill/raw/_index.md
/workspace/wikiskill/wiki/index.md
/workspace/wikiskill/wiki/log.md
/workspace/wikiskill/wiki/skill-impact.md
/workspace/wikiskill/wiki/patterns/
/workspace/wikiskill/skills/active/
/workspace/wikiskill/skills/proposed/
/workspace/wikiskill/skills/archive/
/workspace/wikiskill/bench/train/
/workspace/wikiskill/bench/val/
/workspace/wikiskill/bench/graders/

STATE.md contents:
iteration: 0
R_best: 0
active_skills: []
last_gate: none
next_owner: human

wiki/index.md: one line, "No patterns yet."
wiki/log.md: header "# Wiki log" and today's date.
wiki/skill-impact.md: header "# Skill impact" and a note that rejected proposals stay here forever.

Then post in Loop: workspace ready, iteration 0, waiting for traces and a validation bench.
Do not invent bench tasks. The human must drop held-out tasks into bench/val before any evolve routine runs.
