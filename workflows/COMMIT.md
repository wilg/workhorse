# Commit It

Use only when the user explicitly asks to commit, stage, or write a commit message.

## Match The Ask

- If the user asks only for a commit message, draft the message and stop.
- If the user asks to stage but not commit, stage only the requested paths.
- If the user asks to commit, create the commit.

If the user asks only for a message draft, do not stage, renormalize, or otherwise change the worktree.

## Clarify Scope

If the requested commit scope is ambiguous, use your harness's interactive question tool to ask one short question before staging or committing.

Use it for real choice points such as:
- which logical change to commit
- whether to include or exclude a borderline file
- whether the user wants staging only, a drafted message, or a full commit

Do not ask unnecessary questions when the requested commit scope is already clear.

## Workflow

1. Inspect `git status --short` and pick one logical change.
2. Name the exact paths for that change. Ignore unrelated dirty files.
3. If any targeted file is JSON, run `git add --renormalize -- <json-paths...>` before reading the diff.
4. Review the diff only for the chosen paths.
5. If the repo has relevant tests for the touched area, run them before committing. If the request is only for a message draft, skip validation.
6. Commit with explicit paths and a real message body.

## Guardrails

- Never push.
- One logical change per commit.
- Never use `git add .`, `git commit -a`, or a bare `git commit`.
- Do not amend or rewrite history unless the user asks.
- Do not commit unrelated user changes, generated artifacts, secrets, or machine-local paths.
- Behavior changes need tests.

## Staging Rules

- Prefer `git commit -- <tracked-paths...> -m ...` when every path already exists in git.
- `git commit <paths>` does not stage new untracked files. If the commit includes new files, stage only those explicit paths immediately before commit, in the same shell command, then commit the full path list.
- Keep every staging command path-scoped. Never widen the scope to the whole repo.

Example for tracked files only:

```bash
git commit -- path/to/file1 path/to/file2 -m "$(cat <<'EOF'
Update scene board filters

Tighten the filter logic so archived scenes stop appearing in active views.
This keeps the board aligned with the chapter workflow and removes noise.
EOF
)"
```

Example when new files are included:

```bash
git add -- path/to/new-file.md && \
git commit -- path/to/new-file.md path/to/existing-file.md -m "$(cat <<'EOF'
Add tea house reference note

Capture the new reference note and wire it into the existing scene doc so
the research is committed as one scoped change.
EOF
)"
```

## Message Format

Subject:
- imperative mood
- capital first letter
- no trailing period
- 72 characters max

Body:
- blank line after the subject
- explain why and what
- no step-by-step narration of the diff
- if the reasoning is non-obvious, say it plainly

When drafting a message without committing, return the subject and body as plain text.
