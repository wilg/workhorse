---
name: commit
description: "Commits current changes with a great message."
---

# Commit (Codex)

Read and follow the workflow defined in `COMMIT.md` in this skill's base directory (the directory containing this SKILL.md file).

## Codex specifics

- Codex can ask one concise question if commit scope is genuinely ambiguous. Use a dedicated question UI when the harness exposes one; otherwise ask a short plain-text question in chat. If interruption isn't warranted, pick the most conservative single logical change and document your reasoning in the commit body.
- Respect higher-level repo or session instructions that prohibit commits unless the user explicitly asked for one in the current conversation. When those instructions apply, do not treat nearby planning or implementation approval as commit authorization.
- Keep git commands path-scoped. Run them via shell — the sandbox allows git operations in workspace-write mode.
- Report the final commit hash and full message back to the user.
