---
description: Build it in code. Figma to a local prototype, then a PR as handoff
argument-hint: <project slug, Figma URL, or what to build>
---

Build: **$ARGUMENTS**

Load the `design-engineering` skill.

1. Resolve the project, domain, context and **build target** from its table. Say them:
   > Build · domain `personal` · context `<name>` · target `<repo-name>` · stage local · dispatching design-engineer.
2. Ask the user, in one message, only what the target needs and they have not said
   (where a `new` project lives, the Figma link, any decision the target needs).
3. Load the memory that bears on building: taste for this context and universal,
   `memory/you/growth.md`, and `memory/sources/` for repos, accounts and connectors.
4. Dispatch `design-engineer` for **output 1 (local)** with the task, the user's exact
   request, the target and path, the Figma URL, the project folder, the context file and
   the memory paths.
5. Give the user **the local URL first**, then at most three lines: what is built and
   anything they must decide. Write `decisions.md`; add the location to `project.md`.
6. **Output 2 only on their go.** Dispatch again with "the user approved push and PR".
   Record the PR URL in `project.md`.
7. Motion notes in the report go to memory as `taste` (load `design-memory`). At three
   occurrences, or when asked, write the rule into `.claude/skills/motion-<topic>/`.
