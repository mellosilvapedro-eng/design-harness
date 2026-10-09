---
description: Explore. Either inventory what exists in Figma, or generate divergent directions on a canvas
argument-hint: <figma url | a problem to explore>
---

Explore: **$ARGUMENTS**

Two jobs share this word. Decide which and say so.

**Inventory**: a Figma URL, or "what's already in...". Dispatch `figma-explorer`. Record
every file and library identifier it resolves into `memory/sources/`.

**Divergence**: a problem with no directions yet. Dispatch `design-researcher` first if
`research.md` does not exist, then `design-maker` on `canvas` for two to four directions.
Brief it that the directions must make different bets, each labelled with its bet and
what it trades away. Write `projects/<slug>/directions.md`.
