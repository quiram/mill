# Glossary

Terms mill's skills use throughout and define nowhere else.

**mill** — the package: the whole set of skills for turning agreed work into a usable product. It is the sibling of [winnow](https://github.com/quiram/winnow), which sifts raw input into the requirements mill works from; the two are independent packages that share a theme and a philosophy.

**AI context** — a project's durable documentation: the "advanced README" (`AGENTS.md`, `CLAUDE.md`, `docs/`…) that tells agents how to work on it. mill's skills read it to learn the project's tracker, conventions and workflow.

**Host repo / consuming repo** — the project mill runs *against*, as distinct from this one.

**Default** — what a skill does when the host project's context is silent on something. Always stated to the user and confirmed before use; see [objectives](objectives.md).

**Task** — one unit of implementation work, usually backed by a ticket in the project's tracker but possibly ad hoc.

**Brief** — the description of a task handed to `recommend-model`: the ticket text plus what has been learned about the code it touches.

**Tier** — a class of model by capability and cost (lightweight, standard, frontier, specialised). `recommend-model` reasons in tiers and then maps them to whichever models the host harness actually offers.
