---
description: The front door. Frame what the user is working on, resolve domain, context and surface, and route to the right agents
argument-hint: <what you're working on>
---

The user is working on: **$ARGUMENTS**

If `CLAUDE.md` still contains `{{` placeholders, say so and offer `/design:setup` first.

Load the `design-orchestration` skill.

1. Check `projects/` for an existing project. If one exists, read its `project.md`; it
   declares domain, context, surface and phase.
2. If it is new, resolve the three axes (domain via `context-intake`, context via
   `design-contexts`, surface) and detect the phase from the request.
3. **Say phase, domain, context and surface in one line before dispatching.**
4. Follow `memory/INDEX.md` and load the memory that bears on this phase and context.
5. Dispatch. Independent agents go in one message.

For a genuinely new project, dispatch `context-curator` first (phase `0-context`) unless
the task is self-contained. Then frame in conversation, starting from what the pack
found: the problem, who it is for, what changes if solved, how we would know. Copy
`projects/_template/` to `projects/<slug>/` and write `project.md` and `brief.md` from
real answers.

Do one phase, then offer the next in a line.
