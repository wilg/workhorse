# Commit

When invoked with no further instruction, create a commit.

## Match The Ask

- If invoked with no arguments or just "commit" — create a commit.
- If the user asks only for a commit message, draft the message and stop.
- If the user asks to stage but not commit, stage only the requested paths.

If the user asks only for a message draft, do not stage, renormalize, or otherwise change the worktree.

## Clarify Scope

If the requested commit scope is ambiguous, use your harness's interactive question feature when available; otherwise ask one short in-chat question before staging or committing.

Use it for real choice points such as:
- which logical change to commit
- whether to include or exclude a borderline file
- whether the user wants staging only, a drafted message, or a full commit

Do not ask unnecessary questions when the requested commit scope is already clear.

## Scope

**Bias towards changes from the current conversation.** If the worktree has dirty files beyond what you worked on in this session, assume those are from parallel work and ignore them. Only include files you touched or that the user explicitly asks you to commit.

If the user specifies particular files or a broader scope, follow their instruction instead.

## Workflow

1. Inspect `git status --short`. Identify which changes relate to the current conversation.
2. Name the exact paths for that change. Ignore unrelated dirty files.
3. Review the scoped change cheaply first with `git diff --name-status -- <paths...>` and `git diff --stat -- <paths...>`.
4. If any targeted file is JSON, run `git add --renormalize -- <json-paths...>` before reviewing or committing it.
5. Read full diffs only when needed: ambiguous scope, code behavior changes, generated/secret-like files, surprisingly large stats, or anything you did not edit yourself.
6. Commit with explicit paths and a real message body.

## Fast Path

When the scope is obvious and the change is docs, instructions, tests, comments, deletion of a known file, or a small same-session edit, do not read every line of the full diff. The safe minimum is:

1. `git status --short`
2. `git diff --name-status -- <paths...>`
3. `git diff --stat -- <paths...>`
4. `git diff --check -- <paths...>` for tracked text/code paths when practical
5. path-scoped commit

Do not start broad test or lint runs from this skill unless the user asked for them, the change affects runtime behavior, or no recent relevant verification exists. If checks are skipped, say so plainly after the commit.

## Guardrails

- Never push.
- One logical change per commit.
- Never use `git add .`, `git commit -a`, or a bare `git commit`.
- Do not amend or rewrite history unless the user asks.
- Do not commit unrelated user changes, generated artifacts, secrets, or machine-local paths.
- Behavior changes need tests.
- If `.workhorse/` exists and has changes related to the code being committed (item updates, board moves, knowledge), include them in the same commit.
- Never commit without at least status plus name-status/stat review for the exact paths being committed.

## Staging Rules

- Prefer `git commit -m "..." -- <tracked-paths...>` when every path already exists in git.
- `git commit -- <paths>` does not stage new untracked files. If the commit includes new files, stage only those explicit paths immediately before commit, in the same shell command, then commit the full path list.
- Keep every staging command path-scoped. Never widen the scope to the whole repo.

Example for tracked files only:

```bash
git commit -m "$(cat <<'EOF'
Update scene board filters

Tighten the filter logic so archived scenes stop appearing in active views.
This keeps the board aligned with the chapter workflow and removes noise.
EOF
)" -- path/to/file1 path/to/file2
```

Example when new files are included:

```bash
git add -- path/to/new-file.md && \
git commit -m "$(cat <<'EOF'
Add tea house reference note

Capture the new reference note and wire it into the existing scene doc so
the research is committed as one scoped change.
EOF
)" -- path/to/new-file.md path/to/existing-file.md
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

After committing, output the commit hash and the full commit message so the user can see what was written.

When drafting a message without committing, return the subject and body as plain text.
