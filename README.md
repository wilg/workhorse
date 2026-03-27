# Workhorse

A lightweight, markdown-based work tracker for AI coding agents. State lives in your repo as clean, browsable markdown files. Works across harnesses (Claude Code, Cursor, Codex).

## What it does

- Tracks features, bugs, ideas — no categories, just work items
- Keeps a [board](scaffold/BOARD.md) with Active / Backlog / Ideas / Done
- Each item gets a living document: plan, research, decisions, prereqs, open questions
- Agent researches before implementing, asks you when stuck, commits as it goes
- Context survives across conversations — the item file IS the memory
- Captures [knowledge](scaffold/KNOWLEDGE.md) (hard-won lessons) that persists across items

## Repo structure

```
WORKHORSE.md                  # The workflow — harness-agnostic, this is the brain
harnesses/
  claude-code/SKILL.md        # Thin wrapper: AskUserQuestion, subagents
  cursor/SKILL.md             # Thin wrapper: numbered options, file scans
  codex/SKILL.md              # Thin wrapper: sandbox-aware, front-loads research
scaffold/
  BOARD.md                    # Starter board — copy into your project
  KNOWLEDGE.md                # Starter knowledge file
  items/                      # Where item files go
```

## Setup

### 1. Initialize `.workhorse/` in your project

Copy the scaffold into your project and commit it:

```bash
cp -r /path/to/workhorse/scaffold /path/to/your-project/.workhorse
cp /path/to/workhorse/WORKHORSE.md /path/to/your-project/.workhorse/WORKHORSE.md
cd /path/to/your-project
git add .workhorse && git commit -m "workhorse: initialize board"
```

### 2. Install the harness wrapper

Pick your harness and copy (or symlink) the SKILL.md into the right place.

#### Claude Code (project-level)

```bash
mkdir -p .claude/skills/workhorse
cp /path/to/workhorse/harnesses/claude-code/SKILL.md .claude/skills/workhorse/SKILL.md
```

#### Claude Code (user-level — available in all projects)

```bash
mkdir -p ~/.claude/skills/workhorse
cp /path/to/workhorse/harnesses/claude-code/SKILL.md ~/.claude/skills/workhorse/SKILL.md
```

#### Cursor

```bash
mkdir -p .cursor/skills/workhorse
cp /path/to/workhorse/harnesses/cursor/SKILL.md .cursor/skills/workhorse/SKILL.md
```

#### Codex

```bash
mkdir -p .codex/skills/workhorse
cp /path/to/workhorse/harnesses/codex/SKILL.md .codex/skills/workhorse/SKILL.md
```

### Using symlinks instead

If you want to stay in sync with the workhorse repo without re-copying:

```bash
# Example for Claude Code, project-level
mkdir -p .claude/skills/workhorse
ln -s /path/to/workhorse/harnesses/claude-code/SKILL.md .claude/skills/workhorse/SKILL.md

# And the workflow doc
ln -s /path/to/workhorse/WORKHORSE.md .workhorse/WORKHORSE.md
```

Note: symlinks require the workhorse repo to be present on the machine at the expected path. Copying is more portable.

## Usage

Just talk to your agent naturally:

- "What's on the board?"
- "Let's work on the dialogue system"
- "Add an idea for save/load"
- "What's next?"
- "Where were we?"

No subcommands to learn. The agent reads the board, figures out what you want, and asks when it needs clarification.

## How items work

Ideas are one-liners on the board. When you decide to take one seriously, it gets promoted to a backlog item with its own file. When you pick it up, the agent researches the codebase, writes a plan, and waits for your approval before implementing.

The item file is a **living document** — it gets rewritten as understanding evolves. Git history preserves everything, so the file always reflects current truth.

## License

MIT
