---
description: Prepare handoff. States, edge cases, spec and copy
argument-hint: <project slug | figma url>
---

Handoff: **$ARGUMENTS**

Make everything implicit explicit, so nobody downstream has to guess.

Dispatch `figma-explorer` (or read the code, if the surface is `code`) and
`content-designer` for every user-facing string, in one message.

**If the work was built in code**, the handoff is the PR: once the user says go,
dispatch `design-engineer` for output 2 with the content designer's strings. Still write
`handoff.md` as a copy of what the PR says.

Write `projects/<slug>/handoff.md`:

- **Every state**: empty, first-run, loading, partial, error, permission-denied, one
  item, many, longest string. Say what each looks like.
- **Edge cases** and what happens, including ones nobody asked about.
- **Tokens and components used**, by real name.
- **Copy**: final strings in a table.
- **Open questions**, and who decides.
- **What was deliberately left out.**
