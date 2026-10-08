# AGENTS.md

The index of mill's context. Each entry below says what that document holds — load only the ones the task needs, and file new knowledge where this table says it goes.

| Document | What belongs in it |
| --- | --- |
| [docs/objectives.md](docs/objectives.md) | What mill is for and the properties it is trying to hold: what it must be, what it refuses to do, what "done well" means. |
| [docs/glossary.md](docs/glossary.md) | Terms the skills use throughout and define nowhere else. |
| [docs/task-tracking.md](docs/task-tracking.md) | Which tracker holds work on mill, how to reach it, and any ticket conventions. |
| [docs/ways-of-working.md](docs/ways-of-working.md) | Conventions for changing this repo: commits and releases. |
| [README.md](README.md) | The user-facing surface: what mill is, what a consuming repo can provide, how to install it. |
| [CONTRIBUTING.md](CONTRIBUTING.md) | Everything needed to change mill: repo layout, architectural decisions and their reasoning, the release process. |
| `skills/*/SKILL.md` | A single skill's own behaviour and rules, which live there and nowhere else. |
| `apm.yml` | Package identity, version and the marketplace self-listing. Its description documents how to *use* mill. |

There is no deeper structure under `docs/`, and none is needed until a document exists that no entry above can hold.
