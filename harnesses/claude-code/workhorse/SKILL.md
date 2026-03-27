---
name: workhorse
description: "Track work items, ideas, and progress."
---

# Workhorse (Claude Code)

Start by reading `.workhorse/BOARD.md` in the project root to understand current state.

Read and follow the workflow defined in `WORKHORSE.md` in the same directory as this file.

## Claude Code specifics

- Use **AskUserQuestion** for discrete approvals or scope choices — which item to work on, which approach to take, whether to promote an idea, plan approval. Keep it to one short multiple-choice question when possible.
- Use **TodoWrite** to track progress through multi-step item plans so the user sees live status.
- Start in **Plan mode** for large or ambiguous items, then switch to an execution-capable mode after the user approves the approach.
- Use **Explore** subagents for codebase research and **general-purpose** subagents for deeper cross-cutting investigation so verbose work stays out of the main conversation. Read files directly when you already know what you're looking for.
- Use **WebSearch** and **WebFetch** during the Research phase when the item needs external context — library docs, API references, framework patterns — that the codebase alone can't provide.
- Use **Claude Preview** tools (`preview_start`, `preview_screenshot`, `preview_snapshot`, `preview_click`) to verify UI work against a local dev server. Use **Chrome** tools for broader browser-based verification if available.
- Use **MCP** tools and connectors for external context (issue trackers, monitoring, databases) when they're connected and relevant to the item.
