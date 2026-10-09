---
description: Critique a design from a Figma URL, live URL, repo path or prototype
argument-hint: <figma url | live url | repo path | prototype>
---

Critique: **$ARGUMENTS**

This enters at phase 4 directly.

Resolve the context: critique against the language the work is in. Point the critic at
`projects/<slug>/brief.md` if it exists. Without one, ask the user for one line on what
this is meant to do.

Pass the paths to `memory/critiques/` and `memory/you/growth.md` so recurrences are flagged.

Dispatch `design-critic`. Write `projects/<slug>/critique.md`, then dispatch
`content-designer` if there are copy findings.

**If it is the user's own work**, tally the *kind* of each finding into
`memory/you/growth.md`. Bump existing kinds rather than duplicating. At three, promote
the kind to a pre-flight item and say so.

Carry the critic's limits section through verbatim.
