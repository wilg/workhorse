# Workhorse

Shared skills for AI coding agents. Harness-agnostic workflow docs with thin wrappers for Claude Code, Cursor, and Codex.

## Skills

| Skill | Workflow | What it does |
|-------|----------|-------------|
| [workhorse](workflows/WORKHORSE.md) | Work tracker | Track features, bugs, ideas in browsable markdown |
| [commit](workflows/COMMIT.md) | Scoped commits | One logical change per commit, never pushes |

## Repo structure

```
workflows/
  WORKHORSE.md                      # Work tracker workflow (harness-agnostic)
  COMMIT.md                         # Commit workflow (harness-agnostic)
harnesses/
  claude-code/
    workhorse/SKILL.md              # Thin wrapper + symlinked WORKHORSE.md
    commit/SKILL.md                 # Thin wrapper + symlinked COMMIT.md
  cursor/
    workhorse/SKILL.md
    commit/SKILL.md
  codex/
    workhorse/SKILL.md
    commit/SKILL.md
scaffold/
  BOARD.md                          # Starter board
  KNOWLEDGE.md                      # Starter knowledge file
  items/                            # Where item files go
```

Each harness skill directory is self-contained — the workflow doc is symlinked inside it so you can symlink the whole directory into your harness's skill path.

## Setup

### 1. Initialize `.workhorse/` in your project

```bash
cp -r /path/to/workhorse/scaffold /path/to/your-project/.workhorse
cd /path/to/your-project
git add .workhorse && git commit -m "workhorse: initialize board"
```

### 2. Install skills (user-level — all projects on this machine)

Symlink each skill directory into your harness's user-level skills path:

#### Claude Code

```bash
ln -s /path/to/workhorse/harnesses/claude-code/workhorse ~/.claude/skills/workhorse
ln -s /path/to/workhorse/harnesses/claude-code/commit ~/.claude/skills/commit
```

#### Cursor

```bash
ln -s /path/to/workhorse/harnesses/cursor/workhorse ~/.cursor/skills/workhorse
ln -s /path/to/workhorse/harnesses/cursor/commit ~/.cursor/skills/commit
```

#### Codex

```bash
ln -s /path/to/workhorse/harnesses/codex/workhorse ~/.codex/skills/workhorse
ln -s /path/to/workhorse/harnesses/codex/commit ~/.codex/skills/commit
```

### Project-level install (single project only)

Same pattern but into the project's harness directory:

```bash
# Claude Code example
ln -s /path/to/workhorse/harnesses/claude-code/workhorse .claude/skills/workhorse
ln -s /path/to/workhorse/harnesses/claude-code/commit .claude/skills/commit
```

### Copying instead of symlinks

If you don't want to depend on the workhorse repo being at a specific path:

```bash
cp -r /path/to/workhorse/harnesses/claude-code/workhorse .claude/skills/workhorse
cp -r /path/to/workhorse/harnesses/claude-code/commit .claude/skills/commit
# Also copy the workflow docs since the symlinks won't resolve
cp /path/to/workhorse/workflows/WORKHORSE.md .claude/skills/workhorse/WORKHORSE.md
cp /path/to/workhorse/workflows/COMMIT.md .claude/skills/commit/COMMIT.md
```

## Usage

### Work tracker

Just talk naturally. No commands to remember.

- "What's on the board?"
- "Let's work on the dialogue system"
- "Add an idea for save/load"
- "What's next?"
- "Where were we?"

### Commits

- "Commit this"
- "Draft a commit message"
- "Stage the test changes"

## License

MIT
