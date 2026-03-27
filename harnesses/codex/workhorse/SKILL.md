---
name: workhorse
description: "Track work items, ideas, and progress."
---

# Workhorse (Codex)

For tracked-work requests, start by reading `.workhorse/BOARD.md` in the project root to understand current state. For meta requests about the skill or workflow itself, read the relevant skill and workflow files first and only pull in board context if it will help.

Read and follow the workflow defined in `WORKHORSE.md` in this skill's base directory (the directory containing this SKILL.md file — NOT the project's `.workhorse/` directory).

## Codex specifics

- Codex can communicate during work. Use short progress updates. If the harness exposes Plan mode or a dedicated question UI, use it for substantial approvals; otherwise present the plan in chat and ask one short approval question before implementing. Ask a concise plain-text question only for real blockers or risky choices.
- Front-load research: read the board and active item file at the start, scan the relevant codebase, then present a plan and wait for approval before implementing.
- For large items with nested plans, present the top-level structure for approval first. Detail and implement one branch at a time — don't try to fully plan every branch upfront.
- Use **web search** (cached or live) during the Research phase for external context — library docs, API references, framework patterns. Use **MCP** tools for connected services (issue trackers, monitoring, databases) when relevant.
- Use **parallel subagent threads** for independent research tasks only when the harness and current policy allow delegation and the user has asked for or approved that style of work. Otherwise research directly with shell and file tools.
- Codex has no native browser tool — use **Playwright or Chrome DevTools via MCP** for UI verification when configured. Otherwise verify through automated tests or shell-based checks.
- Write your findings, decisions, and open questions into the item file so the user has full context when reviewing your output. Keep `.workhorse/` updates in sync with related code changes in the worktree, and include them in the same commit when the user explicitly asks for a commit.
- If you hit a blocker or ambiguity that still isn't safe to assume through chat, document it clearly in the item's Open Questions section and stop — don't guess.
