# Workhorse

Workhorse is a lightweight work tracker. State lives in `.workhorse/` in the project root as clean, always-up-to-date markdown files browsable on GitHub.

This document defines the workflow. Skill packages and harness-specific wrappers are thin entry points that point here.

## Core Files

| File | Purpose |
|------|---------|
| `.workhorse/BOARD.md` | The board — single source of truth for all items and status |
| `.workhorse/KNOWLEDGE.md` | Hard-won lessons that apply across items |
| `.workhorse/items/<slug>.md` | One file per real work item — living documents reflecting current truth |

Read `.workhorse/BOARD.md` at the start of every invocation to understand current state. Focus on Active, Backlog, and Ideas — only read Done items if they're relevant to the current work (e.g., for research or understanding prior decisions).

## How You Work

**Research before implementing.** When picking up an item or starting new work:
1. Scan the relevant codebase area (use subagents or your harness's equivalent context-isolation tools to keep verbose output out of chat when available)
2. Write findings into the item's Research section
3. Present a plan in chat and **wait for approval**
4. Only then start implementing

**Keep going until you're done.** Once a plan is approved, the plan IS the authorization. Work through every branch, check off items as you complete them, and move to the next one. The approval already happened — momentum is the default. Stop mid-plan only for real blockers: ambiguity you genuinely can't resolve, a failing build you can't fix, or an open question that needs user input. When you hit a real blocker, update the item's Open Questions and use the harness's interactive question feature (e.g. AskUserQuestion) — this gives the user clearer signal that you're blocked than asking in chat, where it can look like commentary.

**Stay on target through interruptions.** When the user sends messages mid-execution, immediately write anything useful into the item file — update the plan, add open questions, record decisions, or adjust the board. User input mid-execution is volatile; if you don't write it down NOW it will get lost in chat history. Be aggressive about replanning: if the user's input changes the approach, rewrite the plan section to reflect the new reality before resuming work. The approved plan is your anchor, but it's a *living* anchor that absorbs new information. The things that warrant switching away entirely are: an explicit instruction to stop or change tasks, or finishing the current work unit. Everything else gets captured in the item file and you resume.

**Check in between work units.** When you finish the current work unit (all plan items checked off, or the scope the user asked for), use the harness's interactive question feature to ask what's next — offering choices like "Continue to the next item", "Pick something else", or free entry for the user to type whatever they want. Between work units is the natural checkpoint. Mid-unit, keep executing.

**Be conversational.** The user talks naturally. They say "let's work on the dialogue system" or "add an idea for drone cameras" or "what's next?" and you figure out the intent. There are no subcommands to learn or remember.

**Ask interactively when you can.** When you need the user's input — which item to work on, which approach to take, whether to promote an idea — use your harness's interactive question feature when available (for example, AskUserQuestion in Claude Code). If your harness doesn't offer a dedicated question UI, ask a short, concrete question in chat and present clear choices. Don't make the user type long answers when a multiple-choice would do.

**Maintain living documents.** Item files get *rewritten* as understanding evolves. The plan reflects what we know NOW and what's left. Check off completed steps. Refine research as you learn more. Remove things that become irrelevant. Git history preserves everything — files always reflect current truth.

**Commit as you go.** When you update `.workhorse/` files (board, items, knowledge), commit them. When committing code, include relevant `.workhorse/` updates in the same commit so they stay in sync.

**Capture knowledge.** When you learn something that will matter again — a pattern, a gotcha, a project convention — add it to `.workhorse/KNOWLEDGE.md`.

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

Files live in `items/<slug>.md`. A starter template ships at `.workhorse/items/TEMPLATE.md` — copy it when creating a new item. The format:

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
Nest freely — use sub-items to break big work into branches.

- [x] Completed step
- [ ] A larger piece of work
  - [x] Sub-step that's done
  - [ ] Sub-step remaining
    - [ ] Even deeper detail if needed
- [ ] Another top-level step

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
- **Plan** uses nested checkboxes to decompose work into a tree. Top-level items are major branches; sub-items break those down as deep as needed. Check items off as work completes — a parent is checked when all its children are done.
- **Research** is rewritten, not appended — current understanding only
- **Decisions** capture the *why*, not just the *what*
- **Open Questions** get removed when answered (answer goes to Decisions or Plan)
- Omit sections that are empty or not yet relevant
- Keep item files concise. If a section is growing long, rewrite it tighter — the goal is current understanding, not a journal.

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
3. **Plan** — Update the Plan section with concrete steps. For large items, build a nested tree — top-level items are major branches, sub-items break those down. Present the plan in chat.
4. **Ask for approval** — Use the harness's approval flow to confirm the approach: interactive question UI when available, otherwise a short approval question in chat. For large plans, approve the top-level structure first, then detail each branch as you reach it. Do not implement until approved.
5. **Implement** — Work through the plan one branch at a time. Check off steps as you go — check a parent when all its children are done. Commit code + item updates together.
6. **Update the board** — Move between status groups as appropriate.

## Workflow: Completing an Item

1. Confirm all plan steps are checked off. If anything was skipped or descoped, update the plan to reflect reality.
2. Move the item from Active to Done on `.workhorse/BOARD.md`.
3. If you learned something reusable, add it to `.workhorse/KNOWLEDGE.md`.
4. Commit the board and item updates.

## Workflow: Resuming Across Conversations

When the user references an item or says "let's keep working on X":

1. Read `.workhorse/BOARD.md` to find the item.
2. Read the item file — full context: what we know, what's done, what's left, open questions.
3. Briefly summarize where we left off.
4. Pick up from where the plan left off. No re-discovery needed.

## Workflow: Adding Ideas and Items

- **"Add an idea for X"** — Append a one-liner to Ideas on `.workhorse/BOARD.md`. No file.
- **"Let's plan X" / "promote X"** — Create item file, add to Backlog with link, remove from Ideas.
- **"New item: X"** — Create item file, add to Backlog.

When promoting an idea or creating a new item, ask the user to describe what it is and what "done" looks like. Use the harness's question UI when available, otherwise ask a short in-chat clarification if the description is vague.

## Commit Practices

Follow the commit skill's workflow and message format when making commits. Key points:

- Commit `.workhorse/` changes alongside related code changes.
- For board-only changes (adding ideas, reorganizing), commit just `.workhorse/` files.
- One logical change per commit. Don't batch unrelated changes.
- Bias towards changes from the current conversation — ignore unrelated dirty files from parallel work.
- Never push.
