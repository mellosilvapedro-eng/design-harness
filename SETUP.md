# Setup

## For you

1. Open this folder in Claude Code.
2. Connect the tools you already use, if any (Figma, Notion, Slack, a meeting
   transcript tool, an analytics tool, Mobbin). Use `/mcp` or your claude.ai connector
   settings. None are required.
3. Run `/design:setup` and answer the questions. It takes about ten minutes.
4. Read the summary it gives you. Correct anything wrong in one sentence.

You can re-run setup any time. It updates what changed and leaves the rest.

## For the agent running setup

Work in three parts. Ask a few questions at a time, conversationally, not as a form.
Write only inside this folder.

### Part 1: interview

Ask the user:

1. **Who they are.** Name, role, team or company if they want to say it.
2. **How they want to be pushed.** Critique first, or what is working first? What
   should you never do (over-explain, hedge, redesign beyond scope, suggest unasked)?
3. **What they want to get better at** as a designer. This seeds `memory/you/growth.md`.
4. **Domains.** Is there work they do for an employer or client (`work`) and work of
   their own (`personal`)? Which sources belong to each?
5. **Design languages.** Which ones do they work in: their own taste, an employer's
   design system, a client's brand? For each, where is it written down (a skill file, a
   docs site, a token package, a Figma library)? If it is not written down, say so.
6. **Taste in one line.** Ask them to describe their taste in a sentence. Ask whether
   they have a taste skill file and where it lives.
7. **Code.** Where do their repos live? Which ones does design work ship into? What is
   the default stack for a new project? Where do they deploy?
8. **GitHub.** Which accounts are logged into `gh`, and which one belongs to which
   domain? Which commit email belongs to each?
9. **Sources.** Which of these do they use: Slack, Notion, a meeting transcript tool,
   an analytics tool, Figma, Mobbin? Which domain is each one in?

### Part 2: write what you learned

1. **`CLAUDE.md`.** Replace every `{{PLACEHOLDER}}`. Replace the example rows in the
   tables with real rows. Remove any row that does not apply.
2. **`contexts/<name>.md`.** One per design language, copied from
   `contexts/_template.md`. Point at sources by repo-relative path or URL. Never copy
   the language into the file.
3. **`.claude/skills/design-engineering/SKILL.md`.** Fill the build targets table:
   one row per repo, plus `new`. Fill the GitHub account per target.
4. **`.claude/skills/context-intake/SKILL.md`.** Remove adapter rows for sources they
   do not use. Set the domain of each remaining row.
5. **`memory/sources/*.md`.** One file per coordinate set: `repos.md`,
   `github-accounts.md`, `connectors.md`, plus one per tool that needed IDs. Load the
   `design-memory` skill first for the format. Add a line for each to `memory/INDEX.md`.
6. **`memory/you/`.** How they work, and `growth.md` with their own answer to question 3.
   Add index lines.

### Part 3: verify each connector

For every source they named, make **one read-only call** that returns real data, for
example a search for a recent topic, a `whoami`, or a project list. Never post, edit or
create anything.

Record the result per source in `memory/sources/connectors.md`:

```
| Source | Tool present | Read call | Result | Date |
```

Then set the State column in the `context-intake` adapter table to `verified`,
`not connected` or `failing (reason)`. A source is `verified` only after a live call
returned real data. Do not write a coordinate you could not verify.

Finish with a short report: what was filled, what resolved, what did not, and what the
user should connect next.

## Customisation checklist

- [ ] `CLAUDE.md` has no `{{` left
- [ ] Example rows replaced or removed in every table
- [ ] One `contexts/<name>.md` per design language
- [ ] Build targets table filled in `design-engineering`
- [ ] GitHub account per target, and commit email per domain
- [ ] Adapter table in `context-intake` trimmed and states set
- [ ] `memory/sources/` has repos, accounts and connectors, each in `memory/INDEX.md`
- [ ] `memory/you/growth.md` seeded
- [ ] `.mcp.json` created from `.mcp.example.json` if you use project MCP servers
- [ ] Repo set to private if `memory/`, `projects/` or `inbox/` are tracked
