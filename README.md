# Workhorse

Shared skills for AI coding agents that work across harnesses (Claude Code, Cursor, Codex).

**Skills included:**

- **workhorse** — Track work items, ideas, and progress in browsable markdown files checked into your repo. Context survives across conversations. The agent researches before implementing, asks when stuck, and commits as it goes.
- **commit** — Scoped, high-quality commits. One logical change per commit, never pushes.

## Setup

Ask your AI coding agent:

> Install workhorse from https://github.com/wilg/workhorse

That's it. The agent will read the install instructions below and set everything up.

## How it works

### Work tracking

Just talk naturally. No commands to remember.

- "What's on the board?"
- "Let's work on the dialogue system"
- "Add an idea for save/load"
- "What's next?"
- "Where were we on that collision bug?"

Your work lives in `.workhorse/` in your project — a board, item files, and a knowledge base. All markdown, all browsable on GitHub, all committed to git.

Ideas are one-liners on the board. When you take one seriously, the agent creates an item file, researches the codebase, writes a plan, and waits for your approval before implementing. The item file is a living document that gets rewritten as understanding evolves — git history preserves everything.

When you start a new conversation and say "where were we?", the agent reads the board and picks up right where you left off.

### Commits

- "Commit this"
- "Draft a commit message"
- "Stage just the test changes"

## Workflow docs

The harness-agnostic workflow documents define how each skill works:

- [workhorse workflow](workflows/WORKHORSE.md) — Board format, item file format, knowledge capture, how research/plan/implement works
- [commit workflow](workflows/COMMIT.md) — Staging rules, message format, guardrails

## License

MIT

---

## Agent Install Instructions

**You are an AI coding agent installing Workhorse. Follow these steps.**

### 1. Clone the repo

```bash
git clone https://github.com/wilg/workhorse.git ~/Code/workhorse
```

If `~/Code/workhorse` already exists, `git pull` to update instead.

### 2. Initialize `.workhorse/` in the current project

Copy the scaffold into the project root:

```bash
cp -r ~/Code/workhorse/scaffold .workhorse
```

This creates:
- `.workhorse/BOARD.md` — empty board
- `.workhorse/KNOWLEDGE.md` — empty knowledge file
- `.workhorse/items/` — where item files go

Commit it:

```bash
git add .workhorse && git commit -m "workhorse: initialize board"
```

### 3. Install skill symlinks

Detect which harness you are and symlink the matching skill directories into the **user-level** skills path. Each skill directory is self-contained (SKILL.md + symlinked workflow doc).

#### Claude Code

```bash
mkdir -p ~/.claude/skills
ln -sf ~/Code/workhorse/harnesses/claude-code/workhorse ~/.claude/skills/workhorse
ln -sf ~/Code/workhorse/harnesses/claude-code/commit ~/.claude/skills/commit
```

#### Cursor

```bash
mkdir -p ~/.cursor/skills
ln -sf ~/Code/workhorse/harnesses/cursor/workhorse ~/.cursor/skills/workhorse
ln -sf ~/Code/workhorse/harnesses/cursor/commit ~/.cursor/skills/commit
```

#### Codex

```bash
mkdir -p ~/.codex/skills
ln -sf ~/Code/workhorse/harnesses/codex/workhorse ~/.codex/skills/workhorse
ln -sf ~/Code/workhorse/harnesses/codex/commit ~/.codex/skills/commit
```

If the user-level skills directory already has `workhorse` or `commit` entries, remove them first and replace with the new symlinks.

### 4. Verify

Confirm the symlinks resolve:

```bash
cat ~/.claude/skills/workhorse/WORKHORSE.md | head -1
# Should print: # Workhorse
```

(Adjust the path for your harness.)

### 5. Done

Tell the user the skills are installed and available in all projects on this machine. Each project just needs its own `.workhorse/` directory (step 2) to start tracking work.
