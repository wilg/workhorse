# Agent Install Instructions

**You are an AI coding agent installing Workhorse. Follow these steps.**

## 1. Install the skills

Use the standard agent skills CLI:

```bash
npx skills add wilg/workhorse -g --skill '*'
```

If the user wants to install only for a specific agent, include `--agent`:

```bash
npx skills add wilg/workhorse -g --skill '*' --agent codex
npx skills add wilg/workhorse -g --skill '*' --agent claude-code
npx skills add wilg/workhorse -g --skill '*' --agent cursor
```

This installs the public skills from `skills/`:

- `workhorse`
- `commit`
- `scour`

## 2. Initialize `.workhorse/` in the current project

After installation, the `workhorse` skill includes a `scaffold/` directory. When the user asks to initialize Workhorse in a project, create:

- `.workhorse/BOARD.md` from `scaffold/BOARD.md`
- `.workhorse/KNOWLEDGE.md` from `scaffold/KNOWLEDGE.md`
- `.workhorse/items/TEMPLATE.md` from `scaffold/items/TEMPLATE.md`

Commit the scaffold when the user wants the project to start tracking work:

```bash
git add .workhorse/BOARD.md .workhorse/KNOWLEDGE.md .workhorse/items/TEMPLATE.md
git commit -m "workhorse: initialize board" -- .workhorse/BOARD.md .workhorse/KNOWLEDGE.md .workhorse/items/TEMPLATE.md
```

## 3. Verify

List installed skills:

```bash
npx skills list
```

Or verify this repository exposes the expected skills:

```bash
npx skills add wilg/workhorse --list
```
