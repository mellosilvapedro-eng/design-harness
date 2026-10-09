---
name: design-memory
description: The read and write protocol for this harness's memory. How to select what to load, how to write a memory that will be found again, and how to consolidate so the store stays small and true. Load before /design:retro, before any memory write, and when starting a project that may have history.
---

# design-memory

Memory is the difference between a harness and a fresh session with good tools. It is
also the thing most likely to rot. These rules keep it useful.

**Only the orchestrator writes memory.** Agents return findings.

## Reading

`memory/INDEX.md` is imported by `CLAUDE.md`. Load everything else by following a line.
Select by **phase and context**:

- starting a project: `you/`, `sources/`, taste for the active context
- about to make: taste (active and universal), relevant `patterns/`, `you/growth.md`
- about to critique: `critiques/`, taste, `you/growth.md`
- looking for a coordinate: `sources/` **first**, before spending calls on rediscovery

Memory reflects what was true when written. **Verify any path, file, component or URL
before acting on it.** Correct stale ones when you find them.

## Writing

One fact per file. Kebab-case filename. Frontmatter, then the body:

```markdown
---
name: inline-controls-never-cast-shadow
type: taste            # taste | pattern | decision | critique | source | feedback | you
context: <context>     # a context name, or universal
learned: YYYY-MM-DD
occurrences: 1
---

The rule, in one sentence.

**Why:** what happened and the reason the user gave.

**How to apply:** the check to run next time. Related: [[other-memory]]
```

Then **add a line to `memory/INDEX.md`** under the right heading:

```markdown
- [inline controls never cast shadow](taste/inline-controls-never-cast-shadow.md): depth is for floating things only
```

A memory without an index line does not exist. `[[wiki-links]]` to memories not yet
written are fine; they mark something worth writing later.

### What each type is for

| Type | Write it when | Do not write |
|---|---|---|
| `taste` | the user overrode a design decision, or confirmed one against an alternative | a rule already in their taste skill |
| `pattern` | a solution worked and would be reached for again | a one-off |
| `decision` | a real choice with a rejected alternative and a reason | a choice with no alternative |
| `critique` | a finding recurred across different work | every single finding |
| `source` | a coordinate cost real effort to find | anything guessable from the repo |
| `feedback` | the user said how the harness should work | a preference about one design |
| `you` | how the user works, learned from working with them | anything they have not shown you |

Do not write what repos, skills or git history already record, or what only matters to
this conversation.

## The three loops

**Loop 1, in session.** Read the index, load what the phase needs, pass *paths* to agents.

**Loop 2, `/design:retro`.** Extract:

1. what the user **overrode or corrected**: `taste/`, with the why
2. what **worked** and is reusable: `patterns/`
3. **new coordinates**: `sources/`
4. the **decision, its rejected alternative and the reason**: `decisions/`
5. feedback about **how a skill or agent should work**: `feedback/`, and note it for
   `/design:refine-skills`

If a category has nothing, write nothing. An invented lesson poisons the store.

**Loop 3, `/design:memory consolidate`.** Run when the index passes about 40 lines:

- **merge duplicates** into the older file
- **promote on repetition**: three occurrences make a rule; bump `occurrences` instead
  of writing a second file
- **promote across contexts**: a rule that held in two contexts moves to `taste/universal/`
- **prune** what is contradicted, obsolete or no longer resolves
- **delete rather than soften** a memory that was wrong

## you/growth.md

When `design-critic` reviews **the user's own** work, tally each finding here by kind,
not verbatim. When a kind reaches three, promote it to a pre-flight item that
`design-maker` checks before finishing.

Keep it specific ("forgets empty and error states on data screens", not "attention to
detail"). Write it as observation, not verdict.
