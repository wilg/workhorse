---
name: workhorse
description: "Lightweight work tracker. State lives in .workhorse/ markdown files. Use when the user wants to track work, add ideas, check status, plan features, pick up tasks, or discuss what to work on next. Triggers on 'let's work on', 'what's next', 'add an idea', 'status', or references to known work items."
---

# Workhorse (Claude Code)

Read and follow the workflow defined in `.workhorse/WORKHORSE.md`.

## Claude Code specifics

- Use **AskUserQuestion** to present choices interactively — which item to work on, which approach to take, whether to promote an idea, plan approval. Don't make the user type when a multiple-choice works.
- Use **Explore subagents** for codebase research when picking up items. Write findings to the item file, keep verbose output out of the main conversation.
- Use **general-purpose subagents** for deeper cross-cutting investigation.
- Don't over-use subagents for simple tasks. Read files directly when you know what you're looking for.
