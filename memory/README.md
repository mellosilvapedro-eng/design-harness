# Memory

One fact per file, in the folder for its type. Kebab-case filename. Every file gets a
line in `INDEX.md` or it will never be loaded. Only the orchestrator writes here. The
full protocol is in `.claude/skills/design-memory/SKILL.md`.

| Folder | Holds |
|---|---|
| `you/` | how the user works; `growth.md` tallies recurring gaps in their own work |
| `feedback/` | how the user wants the harness to behave |
| `taste/` | design rules learned in one context |
| `taste/universal/` | rules that held in more than one context |
| `patterns/` | solutions worth reaching for again |
| `decisions/` | choices, their rejected alternative, and why |
| `critiques/` | findings that recurred across work |
| `sources/` | verified coordinates: repos, accounts, connectors, ids |

File format:

```markdown
---
name: <kebab-case-name>
type: taste | pattern | decision | critique | source | feedback | you
context: <context name> | universal
learned: YYYY-MM-DD
occurrences: 1
---

The rule or fact, in one sentence.

**Why:** the reason.

**How to apply:** the check to run next time.
```
