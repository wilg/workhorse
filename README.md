# Workhorse

Shared skills for AI coding agents that install through the standard `npx skills` CLI.

**Skills included:**

- **workhorse** — Track work items, ideas, and progress in browsable markdown files checked into your repo. Context survives across conversations. The agent researches before implementing, asks when stuck, and commits as it goes.
- **commit** — Scoped, high-quality commits. One logical change per commit, never pushes.
- **scour** — Long-running codebase sweeps for latent bugs or a requested lens like UX, performance, security, accessibility, tests, or reliability. Opens ready PRs for obvious fixes.

## Setup

Install with the standard agent skills CLI:

```bash
npx skills add wilg/workhorse -g --skill '*'
```

To install only for one agent, pass `--agent`, for example:

```bash
npx skills add wilg/workhorse -g --skill '*' --agent codex
```

Then ask your AI coding agent to initialize Workhorse in a project:

> Initialize workhorse here

The agent will create `.workhorse/` from the scaffold bundled with the installed skill.

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

### Scouring

- "Scour the codebase for latent bugs"
- "Scour auth redirects"
- "Scour perf for the dashboard"
- "Scour UX review checkout"

## Skill packages

Each skill is self-contained under `skills/` so `npx skills add` can install it directly:

- [workhorse](skills/workhorse/SKILL.md) — Includes the workflow doc and project scaffold
- [commit](skills/commit/SKILL.md) — Includes the commit workflow and guardrails
- [scour](skills/scour/SKILL.md) — Includes the long-running review loop and PR rules

## License

MIT

---

**Agent install instructions:** [INSTALL.md](INSTALL.md)
