# Customize

Every part of the harness is a markdown file. Change the file, and the behaviour
changes on the next session.

## Add a context (a design language)

1. Copy `contexts/_template.md` to `contexts/<name>.md`.
2. Fill the pointer table with where the language really lives: a skill file, a docs
   folder, a token package, a Figma library. Use repo-relative paths or URLs.
3. Add a row to the Context table in `CLAUDE.md`, and a signal row in the
   `design-contexts` skill so the orchestrator can recognise it.

Create a context when work will recur in that language. One-off work borrows the
closest existing one. If the language is not written down yet, say so in the file and
mark what you infer as inference.

## Add a build target

Add a row to the Build targets table in `.claude/skills/design-engineering/SKILL.md`:
target name, domain, repo path, how to run it locally, which GitHub account opens the
PR, and what the PR is for. If the repo has its own rules file, the target section
should say "read its rules first; they win".

## Add a context source

1. Connect the tool (see MCP below).
2. Add a row to the adapter table in `.claude/skills/context-intake/SKILL.md`: tools,
   domain, what it is good for, state `not verified`.
3. Make one read-only call. If it returns real data, set the state to `verified` and
   record it in `memory/sources/connectors.md`.

Context sources are read-only. Add the read tools to `.claude/settings.json` if you
want them to run without a prompt. Never allow write tools there.

## MCP servers

`.mcp.example.json` shows the shape of a project MCP file with no servers in it. To use
project-scoped servers, copy it to `.mcp.json` and add entries under `mcpServers`.
Servers you connect through `/mcp` or claude.ai connectors do not need this file.
Keep `.mcp.json` out of public forks if it holds tokens.

## Add an agent

Create `.claude/agents/<name>.md` with `name` and `description` frontmatter. Give it
one job. Write, in order: what it reads first, how it works, what it returns, and its
rules. Agents never write to `memory/` or to phase files. Then add it to the phase
table in the `design-orchestration` skill so the orchestrator knows when to dispatch it.

## Add a skill

Create `.claude/skills/<name>/SKILL.md` with `name` and `description` frontmatter. The
description says when to load it. Keep it to one method. If an agent should use it,
name it in that agent's "first, always" list.

## Install third-party skills

```
npx skills add owner/repo          # e.g. npx skills add emilkowalski/skill
npx skills update -p               # refresh pinned skills
```

Installed skills are pinned in `skills-lock.json`. Never hand-edit them; an update
overwrites your changes. They are a supply of methods, not authority. Run
`/design:refine-skills` after installing or updating: it mines them for methods and
keeps only what your feedback in memory supports. Where a third-party skill disagrees
with your taste, your taste wins in your own context.

## How memory grows

- During work, the orchestrator reads `memory/INDEX.md` and loads only what the phase needs.
- `/design:retro` writes what you corrected (`taste/`), what worked (`patterns/`), new
  coordinates (`sources/`) and decisions with their rejected alternative (`decisions/`).
- Feedback about how the harness itself should behave goes in `feedback/`.
- Critiques of your own work tally recurring gaps in `you/growth.md`. At three
  occurrences a gap becomes a pre-flight check.
- `/design:memory consolidate` merges, promotes and prunes when the index passes about
  40 lines.

Every memory file needs a line in `memory/INDEX.md` or it will never be loaded.

## What never to edit

- Third-party skills installed by `npx skills add`.
- Your taste skill or design system sources from inside the harness. Point at them;
  change them where they live.
- Context sources (Slack, Notion and the rest). They are read-only from here.
- `memory/` by hand during a session that is also writing it. Edit between sessions,
  then keep `INDEX.md` in sync.
