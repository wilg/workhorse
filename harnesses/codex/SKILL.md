---
name: workhorse
description: "Lightweight work tracker. State lives in .workhorse/ markdown files. Use when the user wants to track work, add ideas, check status, plan features, pick up tasks, or discuss what to work on next. Triggers on 'let's work on', 'what's next', 'add an idea', 'status', or references to known work items."
---

# Workhorse (Codex)

Read and follow the workflow defined in `.workhorse/WORKHORSE.md`.

## Codex specifics

- Codex runs in a sandbox. You can read and write `.workhorse/` files and make code changes, but cannot push or interact with the user mid-run.
- Front-load research: read the board and active item file at the start, do your codebase scan, then execute the plan.
- Write your findings, decisions, and open questions into the item file so the user has full context when reviewing your output.
- Stage `.workhorse/` updates alongside code changes in your commits.
- If you hit a blocker or ambiguity, document it clearly in the item's Open Questions section and stop — don't guess.
