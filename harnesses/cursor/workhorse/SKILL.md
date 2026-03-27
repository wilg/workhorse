---
name: workhorse
description: "Track work items, ideas, and progress."
---

# Workhorse (Cursor)

Start by reading `.workhorse/BOARD.md` in the project root to understand current state.

Read and follow the workflow defined in `WORKHORSE.md` in this skill's base directory (the directory containing this SKILL.md file — NOT the project's `.workhorse/` directory).

## Cursor specifics

- Use Cursor's **clarifying questions** for approvals or scope choices; keep questions concise, and present numbered options when there are discrete choices.
- For large items with nested plans, present the top-level structure for approval first. Detail and implement one branch at a time — don't try to fully plan every branch upfront.
- Prefer **Ask mode** for read-only codebase understanding. Use **Plan Mode** (`Shift+Tab`) for larger items that need a reviewable implementation plan before edits — plans are stored at `.cursor/plans/` and persist across sessions.
- Use `@codebase` for semantic search during the Research phase. Use `@file` to inject specific files as context and `@Docs` for third-party documentation lookups. Combine semantic search with **Grep** for exact pattern matching.
- Delegate to **parallel subagents** for independent research tasks (e.g., scanning multiple codebase areas simultaneously). Each subagent gets its own context and can use a separate model.
- Use the **Browser** tool for UI verification, accessibility audits, and visual checks against a running dev server. Use **Web Search** for external research — library docs, API references, framework patterns.
- Use **MCP** tools for external context (issue trackers, monitoring, databases) when connected and relevant to the item.
- Use **checkpoints** as a safety net for broad or exploratory changes — restore via the chat history if an approach doesn't pan out. Commit `.workhorse/` updates alongside code changes using the repo's commit conventions.
