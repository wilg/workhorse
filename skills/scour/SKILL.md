---
name: scour
description: "Long-running codebase scouring for latent bugs or a requested review lens such as UX, performance, security, accessibility, tests, or reliability. Use when the user asks to scour, sweep, hunt for bugs, find latent bugs, open PRs for obvious bugs, or run a broad codebase review with optional scope or process arguments."
---

# Scour

Read and follow the workflow defined in `SCOUR.md` in this skill's base directory (the directory containing this SKILL.md file).

## Agent specifics

- If your harness has a durable goal feature, set a goal whose objective is a complete search of the requested scope with no latent bugs left unhandled.
- Use a plan, todo, or checklist for coverage and PR follow-up. Update it as areas are completed, PRs are opened, and feedback or CI failures are handled.
- Use GitHub tools when available to inspect PR feedback, checks, conflicts, labels, and to open ready PRs. Use `gh` as the shell fallback.
- Do not open draft PRs for this workflow. Label PRs `codex-review-complete` when Codex has run and there is no pending Codex feedback, CI failure, or merge conflict.
- Keep short progress updates flowing during long runs. Continue after each PR unless the goal is complete or a real blocker prevents further progress.
