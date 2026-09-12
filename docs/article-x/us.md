# Grok Bot learns nothing from failure. WikiSkill fixes that inside the product.

Grok Bot already knows how to turn a successful task into a procedure, then turn that procedure into a scheduled run the remote computer will replay even with the laptop shut. That path is in the docs. It holds. It is the path the product designed.

What it cannot do is keep what failed, put it in order, and adopt a new way of working only if that way beats the previous one on a set the worker never saw.

On August 27, 2026, Google Research and Virginia Tech published *WikiSkill: Compiling Agent Experience into Persistent Knowledge for Skill Evolution* (arXiv 2608.27454). It is not a Workspace product. It is a loop with four roles and three layers, and Grok Bot already has the parts.

https://github.com/zepef/wikiskill-grok-bot

## What the paper actually says

Raw traces are never edited. The wiki never rolls back. Procedures roll back when the held-out score does not rise. Workers must not read the wiki: if they do, the score drops from 63.7 to 60.9.

Published results: Gemini-3.5-Flash 49.5% to 68.1%, LiveMath 33 to 72.6, spreadsheet 50.5 to 76.6. A 9B model with evolved procedures beats a 27B model without them.

## The desk

Your workers keep their job. Add Archivist at 2:00, Coach at 2:30, Referee at 3:00. The Loop chat holds those three plus you. No worker enters it.

## Setup

Paste prompts/create-bots.md, then prompts/create-group.md, send prompts/init-workspace.md to Archivist, then after one manual test run paste prompts/create-routines.md.

Paper: https://arxiv.org/abs/2608.27454
