# Agent Install Instructions

**You are an AI coding agent installing Workhorse. Follow these steps.**

### 1. Clone the repo

Pick a location and clone:

```bash
git clone https://github.com/wilg/workhorse.git ~/Code/workhorse
```

If the repo already exists at the chosen path, `git pull` to update instead. Remember the path you used — you'll need it for symlinks below.

### 2. Initialize `.workhorse/` in the current project

Copy the scaffold into the project root (substitute the clone path if different):

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

In the examples below, `$WORKHORSE` is the path where you cloned the repo (e.g. `~/Code/workhorse`).

#### Claude Code

```bash
mkdir -p ~/.claude/skills
ln -sf $WORKHORSE/harnesses/claude-code/workhorse ~/.claude/skills/workhorse
ln -sf $WORKHORSE/harnesses/claude-code/commit ~/.claude/skills/commit
```

#### Cursor

```bash
mkdir -p ~/.cursor/skills
ln -sf $WORKHORSE/harnesses/cursor/workhorse ~/.cursor/skills/workhorse
ln -sf $WORKHORSE/harnesses/cursor/commit ~/.cursor/skills/commit
```

#### Codex

```bash
mkdir -p ~/.codex/skills
ln -sf $WORKHORSE/harnesses/codex/workhorse ~/.codex/skills/workhorse
ln -sf $WORKHORSE/harnesses/codex/commit ~/.codex/skills/commit
```

If the user-level skills directory already has `workhorse` or `commit` entries, remove them first and replace with the new symlinks.

### 4. Verify

Confirm the symlinks resolve (adjust the path for your harness):

```bash
head -1 ~/.claude/skills/workhorse/WORKHORSE.md
# Should print: # Workhorse
```

### 5. Done

Tell the user the skills are installed and available in all projects on this machine. Each project just needs its own `.workhorse/` directory (step 2) to start tracking work.
