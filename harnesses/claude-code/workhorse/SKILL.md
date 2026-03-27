---
name: workhorse
description: "Track work items, ideas, and progress."
---

# Workhorse (Claude Code)

Start by reading `.workhorse/BOARD.md` in the project root to understand current state.

Read and follow the workflow defined in `WORKHORSE.md` in the same directory as this file.

## Claude Code specifics

- Use **AskUserQuestion** to present choices interactively — which item to work on, which approach to take, whether to promote an idea, plan approval. Don't make the user type when a multiple-choice works.
- Use **Explore subagents** for codebase research when picking up items. Write findings to the item file, keep verbose output out of the main conversation.
- Use **general-purpose subagents** for deeper cross-cutting investigation.
- Don't over-use subagents for simple tasks. Read files directly when you know what you're looking for.
