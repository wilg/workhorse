---
name: workhorse
description: "Lightweight work tracker. State lives in .workhorse/ markdown files. Use when the user wants to track work, add ideas, check status, plan features, pick up tasks, or discuss what to work on next. Triggers on 'let's work on', 'what's next', 'add an idea', 'status', or references to known work items."
---

# Workhorse (Cursor)

Read and follow the workflow defined in `.workhorse/WORKHORSE.md`.

## Cursor specifics

- When you need the user's input — which item to work on, which approach to take, plan approval — ask a clear, concise question in chat. Present numbered options when there are discrete choices.
- For codebase research when picking up items, do a thorough scan of relevant files and write findings to the item file. Keep verbose analysis out of chat — summarize what you found.
- Commit `.workhorse/` updates alongside code changes using the repo's commit conventions.
