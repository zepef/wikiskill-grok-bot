# Grok Bot learns nothing from failure. WikiSkill fixes that inside the product.

Grok Bot already knows how to turn a successful task into a skill, then that skill into a scheduled routine the remote computer will replay even with the laptop closed. That path is documented, it holds, and it is exactly the path the product designed.

What it cannot do is keep what failed, put it in order, and adopt a new way of working only if it beats the previous one on a set the worker has not seen.

On 27 August 2026, Google Research and Virginia Tech published *WikiSkill: Compiling Agent Experience into Persistent Knowledge for Skill Evolution* (arXiv 2608.27454). This is not a Workspace product and not a notebook. It is a four-role, three-layer loop, and Grok Bot already has the parts. The pack that wires them together is here:

https://github.com/zepef/wikiskill-grok-bot

## What the paper actually says

The three layers do not live on the same clock, and that is the point of the design.

Raw traces record tool calls, results, successes and failures, and then nobody rewrites them. The wiki collects regularities (root cause, working move, evidence) in an index, a log and an impact register, with no rollback, so a rejected change stays written and is not proposed again. Skills live in SKILL.md files, and those are rolled back as soon as the held-out score stops rising.

Four roles carry that split. Inference does the work with currently enabled skills only. Wiki maintenance distills traces into pages. The proposer writes one create or one patch per cycle. The gate accepts the change only if the validation score beats the best score on record.

Published results speak for themselves: Gemini-3.5-Flash moves from 49.5 percent to 68.1 percent, LiveMath from 33 to 72.6, spreadsheets from 50.5 to 76.6, and a 9-billion-parameter model with evolved skills beats a 27-billion-parameter model without them.

The measurement that matters for Grok Bot is harsher: if the production actor reads the coach wiki, the score drops from 63.7 to 60.9, because traces stop showing the holes in the skill. Workers therefore see only enabled skills, and the wiki stays private to the maintainer and proposer pair.

One more number should be flagged: a skill born from a small model crashed a larger model from 50.5 to 18.1. That is why the impact register exists. It records everything that was tried, accepted or rejected, and why.

## What Grok Bot already gives you

A Bot, in this product, is a job, a memory and a conversation. The shared remote computer (folder /workspace, browser, terminal) keeps running once the laptop screen is closed.

A skill is the how, and six fields are enough to make it useful: when to use it, which inputs and access, which sequence, how to check the result, what to return, and what needs approval. A routine is the when: fifty at most per Bot, twenty stored runs visible.

Enablement is per Bot, under Settings, then Plugins, then Yours. A group chat holds two to six Bots; a slash calls a skill, @ calls a Bot. “Teach a task,” ten minutes at most, seeds the first skill. Approvals, Auto Review, Team Rules and the internal catalog (Teams and Enterprise) close the picture.

The official order does not invert: one task, then a stable skill, then a routine. WikiSkill sits after the stable skill; before that, there is nothing to evolve.

## The gap

A routine history keeps only twenty runs, which is not a raw layer. “Save this as a skill” is not a versioned atomic patch, the product has no built-in validation score, and no per-folder wall stops everyone from seeing /workspace.

Connectors belong to the account, not the Bot, and Bots are not a security boundary: the docs say so plainly. So you do not install WikiSkill as a Google product. You run the algorithm with the parts already in Grok Bot.

## The desk: three Bots, one chat, your workers unchanged

Your workers keep their job. You only add Archivist, Coach and Referee.

Workers do the work, with domain skills, the trace logger and the guard. Archivist keeps the wiki and runs at 2:00. Coach writes one patch per cycle and runs at 2:30. Referee holds the gate and runs at 3:00.

The Loop chat holds Archivist, Coach, Referee and you. No worker enters it: if they watched the wiki being discussed, the isolation the paper describes would be broken. The enablement matrix, under Plugins then Yours, is the real barrier, not the file tree.

## Where the three layers live

```
/workspace/wikiskill/
  raw/YYYY-MM-DD/<bot>-<task>.jsonl
  wiki/{index,log,skill-impact,patterns}/
  skills/{active,proposed,archive}/
  bench/{train,val,graders}/
  STATE.md
```

Skills in service stay in the Grok Bot skill system. /workspace holds evidence, the wiki and quarantine. After accept and your Allow, you use the native command to save or update the skill, then enable it only on the workers who need it; on Teams, you go through the internal catalog.

## The algorithm, inside the product

When the worker finishes a task, the log skill appends one line to the traces, with no secrets and no mail bodies. At 2:00, Archivist reads the day's traces, writes wiki pages, posts a summary in Loop, and does not touch any skill in service. At 2:30, Coach reads the wiki and the impact register, writes one candidate in quarantine, posts the diff in Loop, and enables nothing. At 3:00, Referee runs the held-out set: if the score stays at or below the best score on record, the candidate goes to the archive with a reject row and production does not change; if the score is higher, acceptance waits for your Allow, then come the save and the enablement on workers.

With no held-out set and no grader, Referee stops on “no validation bench.” Starting the loop without that is theater. “Teach a task” seeds the first skill; it is not evolution.

## A Monday morning in a Marketing swarm

Take an ordinary team: three workers already in place, plus the WikiSkill desk described above. Writer drafts the copy. Scout brings topics, rival phrasing, and recurring questions. Publisher stages the post for X and LinkedIn, and never sends without your approval. None of those three enters Loop.

Monday, 11:40. Writer delivers a launch post. The hook promises “free forever.” The live offer, on the page, lasts fourteen days. Publisher follows the current procedure, stages the post, and asks for the green light. Someone approves too fast. The post goes out. The crowd reads it more carefully than the page. Replies pile up, the tone turns, and the correction has to happen in public. At the end of the task, the trace procedure appends one line under `raw/2026-09-14/`: fail, short code `overclaimed-offer`, no post body, no token, no name.

Tuesday, a smaller miss: a preview URL slipped into the body, and a hook already rejected the week before was replayed. Two more traces. Still nothing in the wiki that workers can open.

At 2:00, Archivist reads only the new files. It does not write “be careful with offers.” It writes a pattern page grounded in named traces: symptom, root cause, the move that held, moves already rejected. The impact register gets the same story, so Coach will not propose tomorrow the patch already thrown out. A short summary lands in Loop. Writer does not see it.

At 2:30, Coach does not open three skills “while we are at it.” It takes the hole the wiki documents and that `launch-post` does not cover yet, and it writes one candidate in quarantine: every numbered or absolute promise must cite the offer page before approval is requested, and any hook already marked rejected in the impact register is forbidden. The diff is posted in Loop. Nothing is enabled.

At 3:00, Referee runs eight held-out launches the workers did not see during the week. With the live procedure, five of eight hold. With the candidate, seven of eight hold. The validation score beats the best score on record. Referee does not save anything on its own: it posts accept, scores, and diff, and it waits for your approval. You alone enable the new procedure, and only on Publisher and Writer. Scout does not need it. Publisher, even after that, still does not send without approval.

What the example changes, compared with “we will drop the wiki in a shared folder,” is three refusals. You do not put Writer in Loop “so it improves by itself”: the paper measured that a production actor who reads the trainer wiki makes traces poorer, and the procedure more fragile. You do not let Coach publish. You do not start the nightly runs until the eight held-out launches sit in `bench/val` with a grader: without that set, Referee stops, and the week is only theater.

The next Monday, the same oversized promise does not pass the procedure. The swarm did not “learn marketing.” It stopped paying twice for the same hook.

## Isolation: what holds, what does not

This holds once you combine per-Bot enablement, a closed Loop, wiki / propose / gate skills invisible to the worker, a Team Rule that forbids workers from reading the wiki, and Auto Review that requires approval to save, update or enable a skill, send, delete, or touch production.

This does not hold once you claim Bots are isolated, that a wiki folder will be enough, or that twenty routine records stand in for traces. The real wall, as soon as secrets might enter the traces, remains a second account and a second computer, not a fourth Bot.

## Setup: four pastes, no command line

The repo is here:

https://github.com/zepef/wikiskill-grok-bot

Paste prompts/create-bots.md first, then prompts/create-group.md, send prompts/init-workspace.md to Archivist, and only after a manual test run paste prompts/create-routines.md. Finish with the matrix in TEAM.md under Plugins, Yours, and add the Team Rule.

## What to avoid

Turning wiki maintenance on for a worker “so it improves by itself” is exactly the move the paper measured as a loss. Putting a worker in Loop, trusting the twenty run records, letting Coach enable the skill, folding worker, archivist and coach into one Bot, starting routines before the held-out set exists, or loading eighty domain skills on every Bot just in case: each of those breaks the loop.

## What this changes on Monday

This is not about pretending the machine already knows your files: connectors handle that. This is about stopping the swarm from paying twice for the same mistake, and turning unwritten rules into versioned SKILL.md files, tested and signed by a human before they go live.

The paper also shows that transferred skills often beat skills a model grew on its own. Evolving on Grok Bot and re-gating elsewhere is therefore expected; you still have to re-gate, every time.

MIT pack:

https://github.com/zepef/wikiskill-grok-bot

Paper:

https://arxiv.org/abs/2608.27454

Skills and routines docs:

https://docs.x.ai/grok-bot/skills-routines-and-automations

Find all my digital and AI work in the open at https://le-lab-x.com from today. You can also follow, free of charge, my Grok Bot / SpaceXAI Full Stack course on YouTube and TikTok.
