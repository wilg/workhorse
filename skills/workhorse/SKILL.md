---
name: workhorse
description: "Track work items, ideas, and progress."
---

# Workhorse

For tracked-work requests, start by reading `.workhorse/BOARD.md` in the project root to understand current state. For meta requests about the skill or workflow itself, read the relevant skill and workflow files first and only pull in board context if it will help.

If `.workhorse/` is missing and the user asks to initialize, enable, install, or start using Workhorse in the current project, initialize it from the `scaffold/` directory in this skill's base directory:

- copy `scaffold/BOARD.md` to `.workhorse/BOARD.md`
- copy `scaffold/KNOWLEDGE.md` to `.workhorse/KNOWLEDGE.md`
- copy `scaffold/items/TEMPLATE.md` to `.workhorse/items/TEMPLATE.md`

Read and follow the workflow defined in `WORKHORSE.md` in this skill's base directory (the directory containing this SKILL.md file, not the project's `.workhorse/` directory).

## Agent specifics

- Communicate during work when your harness supports it. Use short progress updates and a plan, todo, or checklist for multi-step work.
- Use an interactive question or approval UI when your harness exposes one. Otherwise ask one concise question in chat for substantial approvals, real blockers, or risky choices.
- Front-load research: read the board and active item file at the start, scan the relevant codebase, then present a plan and wait for approval before implementing.
- For large items with nested plans, present the top-level structure for approval first. Detail and implement one branch at a time; don't try to fully plan every branch upfront.
- Use web search for external context when available and relevant: library docs, API references, framework patterns, and current platform behavior.
- Use connected tools for external services when available and relevant: issue trackers, monitoring, databases, calendars, documents, or GitHub.
- Use browser, preview, Playwright, or Chrome automation for UI verification when configured. Otherwise verify through automated tests or shell-based checks.
- Use parallel subagents or context-isolation tools only when your harness and current policy allow delegation and the task benefits from independent research.
- Write findings, decisions, and open questions into the item file so the user has durable context. Keep `.workhorse/` updates in sync with related code changes in the worktree.
- If you hit a blocker or ambiguity that still isn't safe to assume through chat, document it clearly in the item's Open Questions section and stop.
