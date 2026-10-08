# Objectives

mill exists to take agreed work and carry it towards a usable product. Where the grain has been sifted and the tasks are known, mill is the machinery that processes them: it sets up the work, matches the right tools to it, and hands over to the project's own way of building.

What it is trying to be:

- **Conversational, never autonomous.** Nothing consequential happens until the user has agreed it. The skills recommend and propose; the user decides.
- **Agent-agnostic.** The same skills must work on Claude Code, Copilot, Cursor, Codex and whatever comes next, so nothing may depend on one assistant's mechanisms. Where a harness offers a convenience (a worktree tool, a model switcher), the skills may use it, but they must work without it. It ships through [APM](https://microsoft.github.io/apm/), and this repo is both the package and the marketplace that serves it.
- **Driven by the host project's context.** mill brings no opinion about where a project's tickets live, how it names branches or how it builds. It reads that from the project's own context (`AGENTS.md`, `CLAUDE.md` and the documents they point to) and follows it.
- **Sensible defaults, never silent ones.** When the project's context is silent, the skills fall back to a stated default — and say so. A default is always put to the user for confirmation before it is acted on; it is never simply assumed.
- **Footprint-free in the host project.** Using mill adds no working folders, config files or gitignore entries to a project.
- **Honest about gaps.** Where something needed is missing or ambiguous, the skills surface it rather than inventing a plausible answer.
