---
description: Gather what is already known about a task from chat, docs and transcripts, split into work or personal
argument-hint: <task, project slug, or a link to a thread or doc>
---

Gather context for: **$ARGUMENTS**

Load the `context-intake` skill.

1. If this belongs to a project, read its `project.md` for the domain. Otherwise resolve
   the domain from the signals in `context-intake`. Ask in one sentence if unclear.
2. **Say domain, context and live sources in one line** before dispatching:
   > Context · domain `work` · context `<name>` · chat live, docs live, inbox 2 new · dispatching curator.
3. If the user pasted anything, write it verbatim to `inbox/_new/<YYYY-MM-DD>-<n>.md`.
   Collect any paths and links they gave.
4. Dispatch `context-curator` with the task, paths and links, domain, project folder if
   any, and `memory/sources/connectors.md` to read first.
5. Check the pack against the wall: nothing from `Crossed` goes in. Write it to
   `projects/<slug>/context.md`.
6. Offer the next step in one line, usually framing.
