---
name: workhorse
description: "Track work items, ideas, and progress."
---

# Workhorse (Claude Code)

Start by reading `.workhorse/BOARD.md` in the project root to understand current state.

Read and follow the workflow defined in `WORKHORSE.md` in the same directory as this file.

## Claude Code specifics

- Use **AskUserQuestion** for discrete approvals or scope choices — which item to work on, which approach to take, whether to promote an idea, plan approval. Keep it to one short multiple-choice question when possible.
- Start in **Plan mode** for large or ambiguous items, then switch to an execution-capable mode after the user approves the approach.
- Use built-in **Explore** and **general-purpose** subagents for codebase research and deeper cross-cutting investigation so verbose work stays out of the main conversation.
- Use Claude Code's wider tool surface when it materially helps: **MCP** or connectors for external context, and **Chrome/Desktop browser tools** for UI verification if they are available in the current surface.
- Don't over-use subagents for simple tasks. Read files directly when you know what you're looking for.
