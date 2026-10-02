---
name: preflight
description: Use before scoped or irreversible work, a new feature, a multi-file change, a migration, a ship, a spend, or any automation, cron, hook, bot, or "from now on". Search first, ask at most 3 plan-changing questions with defaults, name the cheapest rung, and offer at most 2 opt-in improvements.
---

# Preflight procedure

Follow `data/gemini-rag/01_OPERATING_RULES.md` for retrieval and output. This skill only adds the ask budget and the rung. Do not dump this file at the user.

## Fill internally
- WHAT, WHERE, WHEN, DELIVERY.
- Non-goals. Reversible or not. Blast radius.
- Assumptions with the default you will use.
- Done-test you will run, not a summary you will write.
- Rung: 1 thread, 2 one file, 3 edit in place, 4 new file on a pattern, 5 new abstraction, 6 research then build. Stop at the first that works.

## Question test
Write both answers. If the work is the same either way, delete the question.
Good: "Replace the handler or add a second route? [default: replace]"
Bad: "Should I follow existing style?" Search, then follow it.
Bad: "Want tests too?" That is an improvement, not a blocker.

## Improvements
Cheaper: fewer tokens, fewer files, or less user time. Same outcome.
Better: one small upgrade. Ignorable.
Banned: a third idea, a rewrite, restating the request.

## Automation
Trigger and what must be true to fire. Second run is a no-op or a safe overwrite. Failure is visible or silent, retry once or stop. One line on what each run spends.

## Examples
"rename foo to bar in this file" → TRIVIAL. No card.
"add export" and one CSV exporter exists → LOCAL. Do it.
Both PDF and CSV exist → one question, default CSV. Cheaper: extend the exporter.
"email me a digest every morning" → IRREVERSIBLE. Do not schedule yet.
1. Which mailbox, and what counts? [default: unread primary, last 24h]
2. What time, and skip if empty? [default: 8:00 local, skip empty]
Cheaper: one daily run that no-ops when empty.
Better: subject line is the count.
"Churches in Concord, NH, names only" → names inside Concord only. No photos, hours, maps, or nearby towns.
