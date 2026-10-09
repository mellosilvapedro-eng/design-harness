# Design Harness

A design studio that runs inside Claude Code. You talk to one orchestrator. It works out
what stage your design work is in, sends specialised agents to do one job each, writes
up what they return, and remembers what you taught it. Everything is plain markdown in
this folder, so you can read, edit and version every part of it.

## The six parts

- **Orchestration**: one orchestrator, eight agents with one job each, a phase model that never forces the full arc.
- **Memory**: a small, indexed store of what you corrected, what worked and what was decided. Only the orchestrator writes to it.
- **Context**: design languages live as pointer files. Agents read your real skills and docs at their source, never a copy.
- **Research**: references read for their reasoning, data read for what it does and does not prove, and a named fallback mode when a source is missing.
- **Canvas**: two to four genuinely different directions side by side, before anything is committed.
- **Code**: a local prototype first, then a pull request as the handoff, only when you say go.

## Folder tree

```
.
├── CLAUDE.md                 orchestrator instructions (filled by setup)
├── SETUP.md                  first-run interview and connector checks
├── CUSTOMIZE.md              how to extend it
├── .claude/
│   ├── agents/               8 specialised agents
│   ├── skills/               8 harness skills (the method)
│   ├── commands/design/      the /design:* commands
│   └── settings.json         read-only permissions
├── .mcp.example.json         where your MCP servers go
├── contexts/                 one pointer file per design language
├── memory/                   INDEX.md plus one file per memory
├── projects/                 one folder per piece of work
├── inbox/                    anything you hand over, filed for you
└── exports/                  files you want to keep out of the repo
```

## Quick start

1. Clone this repo.
2. Open the folder in Claude Code.
3. Run `/design:setup`. Your agent interviews you, fills the placeholders, and checks
   which tools you have connected.

Then run `/design <what you are working on>`.

## How phases work

Work moves through Context, Frame, Understand, Explore, Make, Critique, Handoff and
Learn. Each phase writes one file in `projects/<slug>/`, so the next session knows
where you are. You never have to run them all. A one-off critique enters at Critique
and stops there. The orchestrator offers the next phase in one line and waits.

## Commands

| Command | What it does |
|---|---|
| `/design <task>` | Front door. Resolves domain, context, surface and phase, then routes. |
| `/design:setup` | First run. Interview, placeholders, connector checks. |
| `/design:context` | Gathers what was already said about a task from your sources. |
| `/design:research` | References for a design problem, read for their reasoning. |
| `/design:data` | What the evidence says, or an honest "no quant signal". |
| `/design:explore` | Inventory what exists in Figma, or diverge on a canvas. |
| `/design:make` | Design it in Figma or on a canvas. |
| `/design:build` | Build it in code: local prototype, then a PR on your go. |
| `/design:critique` | Ranked findings with severity and a concrete fix. |
| `/design:handoff` | States, edge cases, spec and copy. |
| `/design:retro` | Writes what was learned to memory. |
| `/design:memory` | Shows or consolidates the memory store. |
| `/design:refine-skills` | Improves the harness skills, filtered by your feedback. |

## Make it yours

The harness ships empty of opinions about your taste. Setup writes who you are into
`CLAUDE.md`, creates a context file for each design language you work in, and records
your tools in `memory/sources/`. From then on, every correction you make in a session
can become a memory, and every memory can sharpen a skill. See `CUSTOMIZE.md` to add
design languages, build targets, sources, agents and skills.

## Keep it private

This template holds no personal data. Once personalised, `memory/`, `projects/` and
`inbox/` hold your work, your taste and possibly your employer's information. Keep your
copy in a private repo. If you want to publish a fork, use the commented lines in
`.gitignore` to keep those folders out.

## Works with other agents

The model is a tool. The method is plain markdown: instructions, skills and memory any
capable coding agent can read. The commands and agent files follow Claude Code
conventions, but nothing here depends on a single vendor.

## License

MIT. See `LICENSE`.
