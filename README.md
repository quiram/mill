<p align="center">
  <img src="assets/logo.svg" alt="mill logo — a windmill grinding grain" width="170"/>
</p>

# mill

Agent skills for turning agreed work into a usable product. They set up a piece of implementation work properly — the right ticket, the right model, a clean branch from an up-to-date base — and hand over to the project's own way of building, agreeing anything they have to assume with the user first.

The package is agent-agnostic: it is distributed with [APM (Agent Package Manager)](https://microsoft.github.io/apm/), so the same skills deploy to Claude Code, GitHub Copilot, Cursor, Codex, and any other harness APM supports. This repo is both the package and the marketplace that serves it.

## Why "mill"?

A mill is where the harvest becomes something you can use. Grain that has been threshed and sifted is no good as it is; the millstones, the sails and the miller's judgement turn it into flour. These skills are that machinery for software: once [winnow](https://github.com/quiram/winnow) has sifted the raw input into requirements, mill takes them and processes them into the final product. The tickets winnow raises are exactly what `start-task` picks up, though neither package requires the other. The logo is a windmill, sails turning.

## The skills

### start-task

The first step of a piece of implementation work. It reads the ticket from the project's tracker, asks `recommend-model` which model suits the task, and creates a fresh branch (in a worktree, where that is the practice) from an up-to-date default branch. It then hands over to the project's own implementation workflow — or, if the project has none, proposes a plan and waits for approval before any code is written.

### recommend-model

Given a task and what is known about the code it touches, recommends the cheapest model that can handle it well: lightweight for mechanical changes, standard for most work, frontier for architectural ambiguity or costly mistakes. It maps that onto the models the user can actually select, and only recommends; switching is the user's call. It also works standalone.

## What a consuming repo can provide

mill reads the host project's context (`AGENTS.md`, `CLAUDE.md` and the documents they point to) to drive its behaviour:

- **The task tracker** and how to reach it.
- **Branch naming** and where branches start from.
- **Worktree practice**, if work happens in worktrees.
- **The implementation workflow** that takes over after setup.
- **Model guidance**, if the project has opinions about cost or which models are available.

None of this is mandatory. Where the context is silent, the skills propose a sensible default and **ask you to confirm it** before acting on it — they never assume and carry on.

## Installing

```bash
apm install quiram/mill
```

See [CONTRIBUTING.md](CONTRIBUTING.md) for working on mill itself.
