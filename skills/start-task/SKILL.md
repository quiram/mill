---
name: start-task
description: >-
  One-off setup for beginning new implementation work: identify the task (read
  its ticket from the project's tracker), get a model recommendation, and open
  a fresh branch from an up-to-date default branch, following the project's own
  conventions and confirming any default it has to assume. Use when the user
  says things like "start a task", "pick up a ticket", "begin work on issue
  #N", or otherwise signals they are about to start new work.
---

# Start task

One-off setup that runs once, before implementation begins. It ends by handing over to the project's own implementation workflow; it never starts writing code itself.

## When to use

The user signals the start of new implementation work: "start a task", "pick up ticket #N", "let's work on issue #N", "begin work on X". Not for mid-task branch corrections.

## Step 0 — Learn the project's conventions

Read the project's AI context (`AGENTS.md`, `CLAUDE.md`, and the documents they point to) for four things:

1. **The task tracker** and how to reach it (CLI, MCP server, API).
2. **Branch naming** and any rules about where branches start from.
3. **Worktree or isolation practice** — whether work happens in worktrees, and where they live.
4. **The implementation workflow** — the process that takes over once setup is done (planning, approval, quality checks, commits).

Anything the context answers, follow. Anything it does not answer, you will need a **default** — and a default is never simply assumed. When you reach the step that needs one, tell the user what the context is silent about, state the default you propose, and wait for them to confirm or replace it. Batch these into a single question where you can.

The defaults, for reference:

| Gap | Default to propose |
|---|---|
| Tracker | None assumed: ask the user which tracker and how to reach it, or whether the work has no ticket. |
| Branch name | `type/<ticket#>-<short-description>` (e.g. `fix/123-login-redirect`), or `type/<short-description>` with no ticket. `type` is one of `feat`, `fix`, `chore`, `docs`, `refactor`. |
| Base branch | The remote's default branch. |
| Isolation | A worktree if the harness offers one; otherwise a plain branch in the current checkout. |
| Implementation workflow | Propose a numbered plan and wait for explicit approval before writing code. |

## Step 1 — Identify the task

- If a ticket was named (or can be inferred from the request), read it through the tracker's tooling. Take the description, acceptance criteria and any linked PR or branch as inputs to everything that follows, not optional context. If the tracker cannot be reached, stop and report precisely what failed.
- If no ticket was named, ask what the task is before continuing. Don't guess. Work with no ticket is fine; just let the user describe it.

## Step 2 — Recommend a model

Skim the code areas the task touches, then invoke **recommend-model** with a brief: the ticket text plus what you found there (how many areas, how well-trodden the patterns, anything risky). If the user has already delegated the model choice (in this request or in the project's context), say so in the brief so recommend-model selects the model without asking; otherwise present its recommendation and let the user confirm or override before continuing, switching models themselves with whatever their harness provides.

If recommend-model cannot be found, say so and proceed: the model choice must never block starting the work.

## Step 3 — Fresh branch from an up-to-date base

Always start from the current tip of the base branch, never from whatever branch happens to be checked out. Do this only after Steps 1–2, because the ticket and model choice may shape the short description in the branch name.

1. **Check the starting state.** `git status --porcelain` must be clean enough to leave behind. If there are uncommitted changes, tell the user and ask what to do; never stash, discard or carry them over silently.
2. **Find and sync the base.** Find the default branch (`git symbolic-ref --short refs/remotes/origin/HEAD`) unless the context names one, then `git fetch origin`. Create the branch from `origin/<base>`, not from a possibly stale local copy.
3. **Create the branch** with the confirmed name, in an isolated worktree if that is the practice in play. If the harness has a worktree facility (for example Claude Code's `EnterWorktree`), prefer it; otherwise use `git worktree add -b <branch> <path> origin/<base>`.
   - Anchor the worktree path at the **main repo root** (absolute path), never relative to the current directory: if you are already inside a worktree, a relative path nests the new one inside it, and removing the outer worktree later orphans the inner one.
   - If the harness refuses because the session is already inside a worktree, don't work around it with a relative path; use the absolute-path form above and then switch into it.
4. **Verify.** Run `git branch --show-current` and confirm it is the intended name. If the tooling named it differently, rename it with `git branch -m <intended-name>` before doing anything else.
5. **Submodules.** If the repo has any (`.gitmodules` exists), run `git submodule update --init --recursive`. A fresh worktree does not populate them, and rules or tooling that import from a submodule fail silently without it. Do this regardless of whether the directories look populated.

## Step 4 — Hand off

Report where things stand: ticket, recommended model, branch, and worktree path if any. Then continue into the implementation workflow found in Step 0. If the project documents none, read the relevant source, produce a numbered implementation plan, and wait for explicit approval before writing any code.
