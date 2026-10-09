---
name: design-contexts
description: Resolve which design language governs a piece of work and load it correctly, from its source and never from a copy. Load before any make, critique or content work, and when adding a design language the harness does not know yet.
---

# design-contexts

A context is a **design language**: whose taste, whose tokens, whose components. It is
separate from the surface. Resolve it first.

## Resolving which context

Fill this table during setup. One row per signal.

| Signal | Context |
|---|---|
| example: a product surface or component from the employer's design system | `<work-context>` |
| example: a personal site, side project, or anything under the user's own name | `<personal-context>` |
| example: a repo path listed in `memory/sources/repos.md` as personal | `<personal-context>` |
| example: a Figma file in the employer's org | usually `<work-context>`; confirm |

Ambiguous cases are real: a side project adjacent to work, an internal tool, a talk
about work. **Ask rather than guess.** Two languages usually disagree on almost
everything, so a wrong guess wastes the run.

## Loading a context

1. Read `contexts/<name>.md`. It is a **pointer file**.
2. Read the skills and docs it points to **at their source**. Those files change without
   this harness knowing; that is why it points instead of copying.
3. Load only what the task needs. The context file says which sources are "always" and
   which are "only when".

Never design from the one-line summary. It tells you which file to open.

## When a source is unreachable

Synced folders may not be downloaded, a checkout may lag, an MCP may be down. **Say so,
and say what you did instead.** A design made from a remembered summary of a design
system is a guess. Degraded is fine when named.

## Adding a context

Copy `contexts/_template.md` to `contexts/<name>.md`, fill it, and add a signal row
above and a row in `CLAUDE.md`. Create one when work will recur in that language.

If the language has no written source yet, say so and record what is **inferred** from
existing work, marked as inference. An inferred rule is a hypothesis until it survives use.

## Contexts and memory

Taste learned in one context does not transfer automatically. `memory/taste/` files
declare their context; `memory/taste/universal/` holds rules that held in more than
one. Those are the valuable ones: taste rather than convention.
