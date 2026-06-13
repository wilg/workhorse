---
name: scour
description: "Long-running codebase scouring for latent bugs or a requested review lens such as UX, performance, security, accessibility, tests, or reliability. Use when the user asks to scour, sweep, hunt for bugs, find latent bugs, open PRs for obvious bugs, or run a broad codebase review with optional scope or process arguments."
---

# Scour (Claude Code)

Read and follow the workflow defined in `SCOUR.md` in this skill's base directory (the directory containing this SKILL.md file).

## Claude Code specifics

- Use TodoWrite to track coverage and PR follow-up.
- Use AskUserQuestion only when a marginal case requires a real human decision before a fix can be PRd.
- Use Explore or general-purpose subagents for independent search areas when useful.
- Use GitHub tooling or `gh` to inspect PR feedback, checks, conflicts, labels, and to open ready PRs.
- Do not open draft PRs. Label PRs `codex-review-complete` when Codex has run and there is no pending Codex feedback, CI failure, or merge conflict.
