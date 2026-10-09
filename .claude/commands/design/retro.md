---
description: Close the loop. Extract what was learned from this work and write it to memory
argument-hint: [project slug]
---

Retro: **$ARGUMENTS**

Load the `design-memory` skill first.

Look back over the conversation, the project files and what the user said. Extract:

1. **What the user overrode or corrected**: `memory/taste/`, tagged with its context, with the why.
2. **What worked and is reusable**: `memory/patterns/`.
3. **New coordinates**: `memory/sources/`. Verify first.
4. **The decision, its rejected alternative and the reason**: `memory/decisions/`.
5. **Feedback about how the harness should work**: `memory/feedback/`, and note it for
   `/design:refine-skills`.

**If a category has nothing, write nothing.** Before writing, check whether a file
already covers it; update it and bump `occurrences`. Delete a memory that turned out wrong.

Every new file gets a line in `memory/INDEX.md`. Tell the user in a few lines what you
learned and what you chose not to record. If the index is past about 40 lines, say
consolidation is due.
