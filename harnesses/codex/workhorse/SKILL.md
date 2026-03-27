---
name: workhorse
description: "Track work items, ideas, and progress."
---

# Workhorse (Codex)

Start by reading `.workhorse/BOARD.md` in the project root to understand current state.

Read and follow the workflow defined in `WORKHORSE.md` in the same directory as this file.

## Codex specifics

- Codex can communicate during work. Use short progress updates, ask a concise plain-text question only for real blockers or risky choices, and use `update_plan` for substantial tasks.
- Front-load research: read the board and active item file at the start, scan the relevant codebase, then execute only after the user approves the plan.
- Use Codex's wider tool surface when it materially helps: browser automation for UI verification, MCP/resources or app connectors for external context, and local skills/plugins when relevant.
- Do not rely on delegated subagents unless the user explicitly asks for delegation; use the harness's own planning, shell, browser, and MCP tools first.
- Write your findings, decisions, and open questions into the item file so the user has full context when reviewing your output, and stage `.workhorse/` updates alongside code changes in your commits.
- If you hit a blocker or ambiguity that still isn't safe to assume through chat, document it clearly in the item's Open Questions section and stop — don't guess.
