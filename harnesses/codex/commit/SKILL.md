---
name: commit
description: "Commits current changes with a great message."
---

# Commit (Codex)

Read and follow the workflow defined in `COMMIT.md` in the same directory as this file.

## Codex specifics

- Codex can ask one concise plain-text question if commit scope is genuinely ambiguous. If interruption isn't warranted, pick the most conservative single logical change and document your reasoning in the commit body.
- Keep git commands path-scoped. Run them via shell — the sandbox allows git operations in workspace-write mode.
- Report the final commit hash and full message back to the user.
