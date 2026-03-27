---
name: commit
description: "Commits current changes with a great message."
---

# Commit (Claude Code)

Read and follow the workflow defined in `COMMIT.md` in the same directory as this file.

## Claude Code specifics

- Use **AskUserQuestion** to clarify commit scope when ambiguous — which logical change, include/exclude borderline files, staging vs drafting vs full commit.
- If Claude Code is in Plan mode, exit it before staging or committing — plan mode is read-only.
- Use `Bash` for all git operations. Use `Read` and `Grep` to inspect diffs — don't pipe git output through shell text tools when dedicated tools work.
