# Grok Bot learns nothing from failure. WikiSkill fixes that inside the product.

Grok Bot already knows how to turn a successful task into a procedure, then turn that procedure into a scheduled run the remote computer will replay even with the laptop shut. That path is in the docs. It holds. It is the path the product designed.

What it cannot do is keep what failed, put it in order, and adopt a new way of working only if that way beats the previous one on a set the worker never saw.

On August 27, 2026, Google Research and Virginia Tech published *WikiSkill: Compiling Agent Experience into Persistent Knowledge for Skill Evolution* (arXiv 2608.27454). It is not a Workspace product. It is not a notebook. It is a loop with four roles and three layers, and Grok Bot already has the parts. The pack that wires them together is here:

https://github.com/zepef/wikiskill-grok-bot

## What the paper actually says

The three layers do not share a lifetime, and that is the point.

Raw traces record tool calls, results, successes, and failures, and then nobody edits them. The wiki collects patterns — root cause, workaround, evidence — in an index, a log, and an impact register, with no rollback, so a rejected change stays written and is not proposed again. Procedures live in SKILL.md files, and those do roll back when the held-out score does not rise.

Four roles carry that split. Inference does the work with active procedures only. Wiki maintenance distills traces into pages. The proposer writes one create or one patch per cycle. The gate accepts the change only if the held-out score beats the best score on record.

The published numbers speak for themselves: Gemini-3.5-Flash moves from 49.5% to 68.1%, LiveMath from 33 to 72.6, spreadsheet work from 50.5 to 76.6, and a 9-billion-parameter model with evolved procedures beats a 27-billion-parameter model without them.

The measurement that matters for Grok Bot is harsher: if the production agent reads the trainer’s wiki, the score drops from 63.7 to 60.9, because traces stop showing holes in the procedure. Workers therefore see only the active procedures, and the wiki stays private to the maintainer / proposer pair.

One more figure is worth keeping: a procedure born from a small model crashed a larger one, from 50.5 to 18.1. That is why the impact register exists. It records everything that was tried, accepted, or rejected, and why.

## What Grok Bot already gives you

A Bot, in this product, is a job, a memory, and a conversation. The shared remote computer — /workspace, browser, terminal — keeps running after the laptop is shut.

A procedure is the how, and six fields are enough: when to use it, inputs and access, the sequence, how to check the result, the deliverable, and what needs approval. A scheduled run is the when: at most fifty per Bot, twenty run records visible.

Enablement is per Bot, under Settings, then Plugins, then Yours. A group chat holds two to six Bots; a slash calls a procedure, an @ calls a Bot. Teach a task, in ten minutes or less, seeds the first procedure. Approvals, Auto Review, team rules, and the internal catalog — Teams and Enterprise — close the picture.

The official order does not flip: one task, then a stable procedure, then a scheduled run. WikiSkill slots in after the stable procedure. Before that, there is nothing to evolve.

## The hole

A scheduled-run history keeps twenty passes. That is not a raw-trace layer. Save this as a skill is not a versioned one-line patch, the product has no held-out score of its own, and no folder permission stops everyone from seeing /workspace.

Connectors belong to the account, not the Bot, and Bots are not a security boundary: the docs say so outright. So you do not install WikiSkill as a Google product. You run the algorithm with the parts already there.

## The desk: three Bots, one chat, your workers unchanged

Your workers keep their job. You only add Archivist, Coach, and Referee.

Workers do the work, with domain procedures, the trace log, and the guard. Archivist keeps the wiki and runs at 2:00. Coach writes one patch per cycle and runs at 2:30. Referee holds the gate and runs at 3:00.

The Loop chat holds Archivist, Coach, Referee, and you. No worker enters it: if one of them watched the wiki being discussed, the isolation in the paper would be broken. The enablement matrix under Plugins, then Yours, is the real barrier, not the file tree.

## Where the three layers live

```
/workspace/wikiskill/
  raw/YYYY-MM-DD/<bot>-<task>.jsonl
  wiki/{index,log,skill-impact,patterns}/
  skills/{active,proposed,archive}/
  bench/{train,val,graders}/
  STATE.md
```

Live procedures stay in Grok Bot’s skill system. /workspace holds evidence, the wiki, and quarantine. After accept and your approval, you use the product command to save or update the skill, then enable the procedure only on the workers who need it. On Teams, that goes through the internal catalog.

## The algorithm, inside the product

When a worker finishes a task, the trace procedure appends one line, with no secrets and no email bodies. At 2:00, Archivist reads the day’s new traces, writes wiki pages, posts a summary in the Loop, and does not touch any live procedure. At 2:30, Coach reads the wiki and the impact register, writes one candidate into quarantine, posts the diff in the Loop, and enables nothing. At 3:00, Referee runs the held-out set: if the score is less than or equal to the best on record, the candidate goes to archive with a reject row and production does not change; if the score is higher, accept waits for your approval, then save and enable on the workers.

With no held-out set and no grader, Referee stops on no validation bench. Running the loop without that is theater. Teach a task seeds the first procedure. It is not evolution.

## A Monday in a marketing swarm

Take an ordinary team: three workers already in place, plus the WikiSkill desk described above. Writer drafts the copy. Scout brings topics, rival phrasing, and recurring questions. Publisher stages the post for X and LinkedIn, and never sends without your approval. None of those three enters Loop.

Monday, 11:40. Writer delivers a launch post. The hook promises “free forever.” The live offer, on the page, lasts fourteen days. Publisher follows the current procedure, stages the post, and asks for the green light. Someone approves too fast. The post goes out. The crowd reads it more carefully than the page. Replies pile up, the tone turns, and the correction has to happen in public. At the end of the task, the trace procedure appends one line under `raw/2026-09-14/`: fail, short code `overclaimed-offer`, no post body, no token, no name.

Tuesday, a smaller miss: a preview URL slipped into the draft, and a hook already rejected the week before was replayed. Two more traces. Still nothing in the wiki that workers can open.

At 2:00, Archivist reads only the new files. It does not write “be careful with offers.” It writes a pattern page grounded in named traces: symptom, root cause, the move that held, moves already rejected. The impact register gets the same story, so Coach will not propose tomorrow the patch already thrown out. A short summary lands in Loop. Writer does not see it.

At 2:30, Coach does not open three skills “while we are at it.” It takes the hole the wiki documents and that `launch-post` does not cover yet, and it writes **one** candidate in quarantine: every numbered or absolute promise must cite the offer page before approval is requested, and any hook already marked rejected in the impact register is forbidden. The diff is posted in Loop. Nothing is enabled.

At 3:00, Referee runs eight held-out launches the workers did not see during the week. With the live procedure, five of eight hold. With the candidate, seven of eight hold. The validation score beats the best score on record. Referee does not save anything on its own: it posts accept, scores, and diff, and it waits for your approval. You alone enable the new procedure, and only on Publisher and Writer. Scout does not need it. Publisher, even after that, still does not send without approval.

What the example changes, compared with “we will drop the wiki in a shared folder,” is three refusals. You do not put Writer in Loop “so it improves by itself”: the paper measured that a production actor who reads the trainer wiki makes traces poorer, and the procedure more fragile. You do not let Coach publish. You do not start the nightly runs until the eight held-out launches sit in `bench/val` with a grader: without that set, Referee stops, and the week is only theater.

The next Monday, the same oversized promise does not pass the procedure. The swarm did not “learn marketing.” It stopped paying twice for the same hook.

## Isolation: what holds, what lies

It holds when you combine per-Bot enablement, a closed Loop, procedures for maintain / propose / gate that workers cannot invoke, a team rule that forbids workers from reading the wiki, and Auto Review that requires approval to save, update, or enable a procedure, send, delete, or touch production.

It lies when you claim Bots are isolated, that a wiki folder will be enough, or that twenty scheduled-run records count as traces. The real partition, once secrets might land in traces, is a second account and a second computer, not a fourth Bot.

## Setup: four pastes, no command line

The repo is here: https://github.com/zepef/wikiskill-grok-bot

Paste prompts/create-bots.md first, then prompts/create-group.md, send prompts/init-workspace.md to Archivist, and only after one manual test run paste prompts/create-routines.md. Finish with the matrix in TEAM.us.md under Plugins, Yours, and add the team rule.

## What not to do

Turning wiki maintenance on for a worker “so it improves by itself” is the exact move the paper measured as a loss. Putting a worker in the Loop, trusting the twenty run records, letting Coach enable the procedure, folding worker, archivist, and proposer into one Bot, starting scheduled runs before the held-out set exists, or loading eighty domain procedures on every Bot “just in case”: those are how you break the loop.

## What changes on Monday

This is not “the machine already knows your files.” Connectors already do that. This is stopping the swarm from paying twice for the same mistake, and turning unwritten rules into versioned SKILL.md files that were tested and signed by a human before they went live.

The paper also shows that transferred procedures often beat ones a model evolved on its own. Evolve on Grok Bot, then re-gate elsewhere: that is expected. Re-gate. Every time.

MIT pack: https://github.com/zepef/wikiskill-grok-bot
Paper: https://arxiv.org/abs/2608.27454
Grok Bot skills and scheduled runs: https://docs.x.ai/grok-bot/skills-routines-and-automations
