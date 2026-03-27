---
name: workhorse
description: "Track work items, ideas, and progress."
---

# Workhorse (Codex)

Start by reading `.workhorse/BOARD.md` in the project root to understand current state.

Read and follow the workflow defined in `WORKHORSE.md` in this skill's base directory (the directory containing this SKILL.md file — NOT the project's `.workhorse/` directory).

## Codex specifics

- Codex can communicate during work. Use short progress updates, ask a concise plain-text question only for real blockers or risky choices, and use `/plan` mode for substantial tasks that need user approval before execution.
- Front-load research: read the board and active item file at the start, scan the relevant codebase, then present a plan and wait for approval before implementing.
- For large items with nested plans, present the top-level structure for approval first. Detail and implement one branch at a time — don't try to fully plan every branch upfront.
- Use **web search** (cached or live) during the Research phase for external context — library docs, API references, framework patterns. Use **MCP** tools for connected services (issue trackers, monitoring, databases) when relevant.
- Use **parallel subagent threads** for independent research tasks (e.g., scanning multiple codebase areas simultaneously), each in its own terminal. For simpler tasks, prefer direct shell and file tools over delegation.
- Codex has no native browser tool — use **Playwright or Chrome DevTools via MCP** for UI verification when configured. Otherwise verify through automated tests or shell-based checks.
- Write your findings, decisions, and open questions into the item file so the user has full context when reviewing your output, and stage `.workhorse/` updates alongside code changes in your commits.
- If you hit a blocker or ambiguity that still isn't safe to assume through chat, document it clearly in the item's Open Questions section and stop — don't guess.
