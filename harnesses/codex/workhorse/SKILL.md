---
name: workhorse
description: "Track work items, ideas, and progress."
---

# Workhorse (Codex)

Start by reading `.workhorse/BOARD.md` in the project root to understand current state.

Read and follow the workflow defined in `WORKHORSE.md` in the same directory as this file.

## Codex specifics

- Codex runs in a sandbox. You can read and write `.workhorse/` files and make code changes, but cannot push or interact with the user mid-run.
- Front-load research: read the board and active item file at the start, do your codebase scan, then execute the plan.
- Write your findings, decisions, and open questions into the item file so the user has full context when reviewing your output.
- Stage `.workhorse/` updates alongside code changes in your commits.
- If you hit a blocker or ambiguity, document it clearly in the item's Open Questions section and stop — don't guess.
