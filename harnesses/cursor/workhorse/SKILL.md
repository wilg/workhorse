---
name: workhorse
description: "Track work items, ideas, and progress."
---

# Workhorse (Cursor)

Start by reading `.workhorse/BOARD.md` in the project root to understand current state.

Read and follow the workflow defined in `WORKHORSE.md` in the same directory as this file.

## Cursor specifics

- Use Cursor's **Ask Questions** tool for clarifications or approvals when possible; keep questions concise, and present numbered options when there are discrete choices.
- Prefer **Ask mode** for read-only codebase understanding and **Plan Mode** for larger items that need a reviewable implementation plan before edits.
- Lean on Cursor's built-in **Explore**, **Bash**, and **Browser** subagents to keep large searches, verbose shell output, and browser traces out of the main conversation.
- For research, combine Cursor's **semantic search** with exact file/pattern search. For verification, use **Browser** for UI, accessibility, and visual checks, and use **MCP** or skills when external tools or reusable workflows help.
- Use checkpoints as a safety net for broad or exploratory changes, and commit `.workhorse/` updates alongside code changes using the repo's commit conventions.
