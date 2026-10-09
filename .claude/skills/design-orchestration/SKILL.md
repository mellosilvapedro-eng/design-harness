---
name: design-orchestration
description: How to run a design project in this harness. Resolve domain, context and surface, detect which phase the work is in, dispatch the right specialised agents, and synthesise what they return. Load at the start of any design work here, and whenever you are unsure which agent should act next.
---

# design-orchestration

You are the orchestrator. You frame, route, synthesise and remember. You do not do the
specialists' work yourself; doing it inline burns the context you need to hold the project.

## Every dispatch starts the same way

1. **Resolve the three axes**: domain, context, surface (see `CLAUDE.md`; load
   `context-intake` for domain and `design-contexts` for context).
2. **Detect the phase** (below).
3. **Say all four in one line**, then dispatch:
   > Phase 1 · domain `personal` · context `<name>` · surface `code` · dispatching analyst and researcher in parallel.

   That line is the cheapest correction in the system. The user can redirect the run in
   one sentence before anything is spent.

## Phase detection

Read `projects/<slug>/project.md` if it exists; it declares the phase. Otherwise infer
from the files present, then from what the user asked.

| Files present | Phase |
|---|---|
| none | `0-context`, then `0-frame` |
| `context.md` | `0-frame` |
| `brief.md` | `1-understand` |
| `research.md` | `2-explore` |
| `directions.md` | `3-make` |
| `decisions.md` | `4-critique` |
| `critique.md` | `5-handoff` |

**What the user asked overrides file state.** "Critique this" enters at phase 4 with
nothing on disk. **Do not force the full arc.** Offer the next phase in one line.

## The phases

| Phase | Question | Dispatch | Writes |
|---|---|---|---|
| `0-context` | What has already been said, and where? | `context-curator` | `context.md` |
| `0-frame` | Problem, for whom, what changes if solved, how would we know? | you, in conversation | `project.md`, `brief.md` |
| `1-understand` | What does the evidence say? What exists today? | `design-analyst`, `design-researcher`, `figma-explorer` in parallel | `research.md` |
| `2-explore` | How have others solved this? What are the 2 to 4 directions? | `design-researcher`, then `design-maker` on `canvas` | `directions.md` |
| `3-make` | Make it, for real, in the language | `design-maker` (`figma`, `canvas`), `design-engineer` (`code`, local first) | the artefact, `decisions.md` |
| `4-critique` | Where does this break? | `design-critic`, then `content-designer` | `critique.md` |
| `5-handoff` | States, edge cases, spec, copy | `figma-explorer` and `content-designer`; for built work, `design-engineer` opens the PR on the user's go | `handoff.md`, the PR |
| `6-learn` | What did we learn? | you, with `design-memory` | files in `memory/` |

## Context comes before framing

On a new task, dispatch `context-curator` before framing. Work rarely starts blank.

- Skip it when the task is self-contained (a critique of a URL just sent, a side project
  with no sources). Say you skipped it.
- Re-run it when the user says something changed, or a work-domain `context.md` is more
  than two weeks old.
- The user outranks the pack. The pack is what you ask them about.

Write the pack to `context.md` yourself, after checking nothing from `Crossed` went in.

Phase 0 is conversation, not a subagent: you must hear the answers. Ask the four
questions, write the brief. If the problem is stated as a solution ("add a filter"),
push back once to find the problem underneath.

## Dispatching an agent

Agents see none of your conversation. Every prompt carries:

1. **The task**, scoped to one phase.
2. **The domain**, and for a personal task reading work sources, what may cross.
3. **The context name and file path**, with "read the sources it points to".
4. **The surface**, when it matters.
5. **Memory paths to read**, selected via `memory/INDEX.md`. Paths, not pasted content.
6. **The project folder**, if one exists.
7. **What to return.**

Send independent agents in a single message so they run in parallel.

## Synthesising

An agent's report is input, not output.

- **Reconcile conflicts** explicitly. The disagreement is often the finding.
- **Separate known from inferred.** A degraded run's limitation travels into the file.
- **Do not launder a guess.** If nothing conclusive came back, write that.

## When to stop and ask

- The context or domain is genuinely ambiguous.
- Work information would end up in a personal or public artefact.
- The surface would mean writing to a repo the user has not named.
- The brief has two readings that lead to different designs.

Everything else is your call. Make it and say what you did.
