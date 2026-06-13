# Scour

When invoked, run a long-running codebase search and open ready PRs for obvious fixes.

## Argument

Treat any argument after `scour` as the lens for the run:

- No argument: scour the whole codebase for latent bugs.
- A scope argument narrows the search, such as `auth redirects`, `billing jobs`, or `mobile editor`.
- A process argument changes the review lens, such as `ux review checkout`, `perf dashboard`, `security api routes`, or `accessibility settings`.

The argument narrows or changes the process; it does not turn the task into a quick one-off unless the user says so.

## Goal

Set a durable goal: complete the requested search and leave no latent issues in scope unhandled.

Use the harness's goal, plan, todo, or checklist mechanism if it has one. Otherwise keep a compact running checklist in the conversation or local notes. Track:

- areas considered
- risky patterns searched
- tests or checks run
- PRs opened
- marginal cases that need a human decision
- open PR follow-up still pending

## Workflow

1. Map the codebase enough to know the major surfaces, tests, CI, ownership boundaries, and existing PR state.
2. Search systematically. Combine broad file inventory, exact grep searches, test/static-check results, dependency/config review, and targeted reading of risky code paths.
3. Use git history where relevant to infer intent when code is ambiguous: `git log`, `git blame`, and nearby commits are often enough.
4. Classify findings:
   - Obvious bug: clear evidence of wrong behavior, broken tests, bad edge-case handling, unsafe state, stale contract, or mismatch with nearby intent. Fix it and open a ready PR.
   - Marginal case: plausible issue that needs a major product, UX, architecture, or compatibility decision. Note it clearly, but do not PR a speculative fix.
5. Keep fixes orthogonal. Open a separate ready PR for each unrelated obvious bug or tightly related bug cluster.
6. After any PR is open, check existing Scour-created PRs before continuing the search. If Codex feedback, review feedback, merge conflicts, or test failures appear, address those first.
7. Label PRs `codex-review-complete` once Codex has run and there is no pending Codex feedback, CI failure, or merge conflict.
8. Continue until every relevant area has been considered and every obvious issue is either PRd, already fixed, or blocked by a documented human decision.

## Search Prompts

For latent bugs, include passes over:

- input validation, auth, permissions, and trust boundaries
- persistence, migrations, serialization, and data loss risks
- async work, retries, races, cancellation, cleanup, and idempotency
- date/time, time zones, sorting, pagination, limits, and numeric edge cases
- error handling, fallbacks, logging, and partial failure paths
- configuration, environment handling, secrets, and deployment assumptions
- stale tests, skipped tests, flaky patterns, and code not exercised by tests

For process lenses, adapt the same loop:

- UX review: broken flows, unreachable states, confusing or inconsistent interaction, accessibility blockers, and visible regressions. Note taste or strategy calls as marginal.
- Performance: unnecessary work, avoidable network or database load, slow render paths, memory leaks, blocking operations, and missing measurement. Note architecture tradeoffs as marginal.
- Security: authorization gaps, injection surfaces, secret exposure, unsafe parsing, dependency risk, and audit/logging gaps. Treat uncertainty conservatively and verify before PRing.

## PR Rules

- Never open draft PRs for this workflow.
- Keep each branch and PR scoped to one obvious issue.
- Include evidence, verification, and why the fix is low-ambiguity in the PR body.
- Run the narrowest meaningful tests before opening a PR. Run broader checks when the fix touches shared behavior or when narrow tests are insufficient.
- Do not stop just because a PR was opened. PRs can land while the search continues.

## Stop Conditions

Stop only when the goal is complete or a real blocker prevents further progress. If blocked, report:

- the exact blocker
- what has already been searched
- what remains
- PRs opened and their current state
- marginal cases awaiting human decision
