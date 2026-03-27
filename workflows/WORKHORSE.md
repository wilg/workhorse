# Workhorse

Workhorse is a lightweight work tracker. State lives in `.workhorse/` as clean, always-up-to-date markdown files browsable on GitHub. All links use relative markdown links for GFM compatibility.

This document defines the workflow. Harness-specific skills (Claude Code, Cursor, etc.) are thin wrappers that point here.

## Core Files

| File | Purpose |
|------|---------|
| [BOARD.md](BOARD.md) | The board — single source of truth for all items and status |
| [KNOWLEDGE.md](KNOWLEDGE.md) | Hard-won lessons that apply across items |
| `items/<slug>.md` | One file per real work item — living documents reflecting current truth |

Read [BOARD.md](BOARD.md) at the start of every invocation to understand current state.

## How You Work

**Be conversational.** The user talks naturally. They say "let's work on the dialogue system" or "add an idea for drone cameras" or "what's next?" and you figure out the intent. There are no subcommands to learn or remember.

**Ask interactive questions.** When you need the user's input — which item to work on, which approach to take, whether to promote an idea — use your harness's interactive question feature (e.g. AskUserQuestion in Claude Code) to present clear choices. Don't make the user type long answers when a multiple-choice would do.

**Maintain living documents.** Item files get *rewritten* as understanding evolves. The plan reflects what we know NOW and what's left. Check off completed steps. Refine research as you learn more. Remove things that become irrelevant. Git history preserves everything — files always reflect current truth.

**Commit as you go.** When you update `.workhorse/` files (board, items, knowledge), commit them. When committing code, include relevant `.workhorse/` updates in the same commit so they stay in sync.

**Research before implementing.** When picking up an item or starting new work:
1. Scan the relevant codebase area (use subagents to keep verbose output out of chat)
2. Write findings into the item's Research section
3. Present a plan in chat and **wait for approval**
4. Only then start implementing

**Stop when stuck.** If you hit ambiguity, a blocker, or need the user's input, update the item's Open Questions and ask in chat. Don't guess.

**Capture knowledge.** When you learn something that will matter again — a pattern, a gotcha, a project convention — add it to [KNOWLEDGE.md](KNOWLEDGE.md).

## BOARD.md Format

```markdown
# Board

## Active
- [slug](items/slug.md) — Short description of what this is

## Backlog
- [slug](items/slug.md) — Short description

## Ideas
- Just a string describing a vague idea (no file yet)

## Done
- [slug](items/slug.md) — Short description
```

- **Active** — Currently being worked on. Usually 1 item, sometimes 2 if independent.
- **Backlog** — Decided to do, has its own item file, not started yet.
- **Ideas** — Just strings. No files. Promoted to Backlog when we take them seriously.
- **Done** — Completed. Keep the link for reference.

## Item File Format

Files live in `items/<slug>.md`. Use this template:

```markdown
# Title

## What
What this is and why it matters. Updated as understanding deepens.

## Prereqs
- [other-item](other-item.md) (done)
- [blocking-item](blocking-item.md) (backlog)

Or "None" if no prerequisites.

## Plan
Current plan. Always reflects what we know NOW and what's left.

- [x] Completed step
- [ ] Next step
- [ ] Future step

Key files: `Path/To/Relevant/File.cpp`, `Another/File.h`

## Research
What we learned about the codebase, patterns, constraints.
Rewritten as understanding evolves — not appended.

## Decisions
- **Decision**: Rationale — why we chose this over alternatives

## Open Questions
- Unresolved questions that need input or investigation
```

- **Prereqs** link to other item files: `[slug](slug.md)`
- **Plan** checkboxes reflect actual progress — check them off as work completes
- **Research** is rewritten, not appended — current understanding only
- **Decisions** capture the *why*, not just the *what*
- **Open Questions** get removed when answered (answer goes to Decisions or Plan)
- Omit sections that are empty or not yet relevant

## KNOWLEDGE.md Format

```markdown
# Knowledge

Lessons learned that apply across work items.

- **Short title**: What we learned and why it matters.
  Discovered while working on [item](items/item.md).
```

- Flat list, no categories
- Link back to the item where it was discovered
- Only things that will matter again — not a changelog

## Workflow: Picking Up an Item

1. **Read the item file** (or create one if promoting from Ideas or new work).
2. **Research** — Scan the relevant codebase. Update the Research section.
3. **Plan** — Update the Plan section with concrete steps. Present in chat.
4. **Ask for approval** — Use interactive questions to confirm the approach. Do not implement until approved.
5. **Implement** — Work through the plan. Check off steps. Commit code + item updates together.
6. **Update the board** — Move between status groups as appropriate.

## Workflow: Resuming Across Conversations

When the user references an item or says "let's keep working on X":

1. Read [BOARD.md](BOARD.md) to find the item.
2. Read the item file — full context: what we know, what's done, what's left, open questions.
3. Briefly summarize where we left off.
4. Pick up from where the plan left off. No re-discovery needed.

## Workflow: Adding Ideas and Items

- **"Add an idea for X"** — Append a one-liner to Ideas on [BOARD.md](BOARD.md). No file.
- **"Let's plan X" / "promote X"** — Create item file, add to Backlog with link, remove from Ideas.
- **"New item: X"** — Create item file, add to Backlog.

When promoting an idea or creating a new item, ask the user to describe what it is and what "done" looks like. Use interactive questions to clarify scope if the description is vague.

## Commit Practices

Follow the [commit](COMMIT.md) skill's workflow and message format when making commits. Key points:

- Commit `.workhorse/` changes alongside related code changes.
- For board-only changes (adding ideas, reorganizing), commit just `.workhorse/` files.
- One logical change per commit. Don't batch unrelated changes.
- Bias towards changes from the current conversation — ignore unrelated dirty files from parallel work.
- Never push.
