---
name: design-engineering
description: How design gets built in code here. The build targets, the two outputs every build produces (a local prototype to look at, then a PR), the Figma-to-code fidelity loop, the PR-as-handoff format, and how motion rules grow from the user's feedback. Load before dispatching design-engineer, before /design:build, and when adding a build target.
---

# design-engineering

The design engineer makes the Figma **real**: as close as the target allows, with the
motion and states Figma cannot show. It works only in code. Figma and canvas stay with
`design-maker`.

## Two outputs, always in this order

1. **Local**: a running prototype the user can open, a `localhost` URL verified to load.
   This is where the design gets judged. Nothing goes to GitHub before the user has seen it.
2. **GitHub**: a branch, commits and a PR whose description is the handoff. **Push and
   PR only after the user says go** for this build. A PR is outward-facing: someone
   else reads it, CI runs on it, some repos deploy on merge.

The engineer stops after output 1 and returns the URL. Output 2 is a second dispatch
with the user's go.

## Build targets

Setup fills this table. Resolve the target before anything else. Paths are
repo-relative to where the user keeps code, or recorded in `memory/sources/repos.md`.

| Target | Domain | Path | Local | GitHub account | The PR is |
|---|---|---|---|---|---|
| `<repo-name>` (example) | personal | `<path>` | `<dev command>` then `<local URL>` | `<personal account>` | the user's own change, merged by them |
| `<team-repo>` (example) | work | `<path>` | `<dev command>` then `<local URL>` | `<work account>` | a handoff to a developer |
| `new` | either | ask the user | scaffolded dev server | by domain; ask for work | first commit, then deploy |

Synced or network folders can be slow to materialise. A hanging read means "unknown",
not "gone".

### GitHub accounts: the wrong one is a real leak

If more than one account is logged into `gh`, never switch the global active account.
Scope it per command:

```
GH_TOKEN=$(gh auth token -u <personal-account>) gh pr create ...
GH_TOKEN=$(gh auth token -u <work-account>)     gh pr create ...
```

Check `git config user.email` before the first commit. A new personal repo sets its
local email to the personal one before its first commit. A work email on a public
personal repo cannot be taken back. Accounts and emails per domain live in
`memory/sources/github-accounts.md`.

### Any existing repo

The repo governs. Read its `CLAUDE.md` or `AGENTS.md` every time, then the files around
the change, and match them. Use its tokens and components; if a token is missing, add it
where the others live. If it has a prototyping CLI or lifecycle scripts, use them; never
hand-edit generated metadata. Run its gates (typecheck, lint, tests, any preflight)
before a PR and report the output.

- **Never disturb the user's checkout.** If `git status` is not clean or the branch is
  not the default, work in a worktree:
  `git worktree add ../<repo>-wt/<slug> -b <prefix>/<slug> origin/<default>`, then
  install there. Never stash, reset or switch branches in their checkout.
- **Pull the default branch first.**
- Branch `<prefix>/<slug>`; never commit to the default branch.
- If the target needs a decision before editing (a new version or the current one, a
  folder), the orchestrator asks the user and passes the answer. No answer, no edit.
- Never write to folders the repo marks as framework-owned or vendored.

### `new`

Ask where it lives. Use the user's default stack from `memory/sources/repos.md`.
Scaffold, `git init`, set the local email, build, run. Deploy with the user's deploy
target (for example Vercel). If the CLI needs a login, the user does it. Do not claim a
deploy until a URL answers.

## The Figma fidelity loop

Read the Figma properly, not a screenshot and a guess.

1. Load the Figma design-to-code skill before `get_design_context`, and the motion skill
   if the node has motion.
2. Per frame: `get_design_context` (structure), `get_variable_defs` (tokens),
   `get_screenshot` (the target), `get_code_connect_map` (existing component mappings).
3. **Map before building.** Every element to a real component and token, from the
   design system's docs or the repo's own components. Anything unmatched becomes a
   **named standalone component**, not something hidden inside a page.
4. **Build, then compare** element by element: spacing, type, colour, radius, states.
   Record every deliberate deviation and its reason.
5. **Fill Figma's blind spots**: hover, press, focus, loading, empty, error, long
   strings, both themes, reduced motion. Stress with worst-case data. List which states
   Figma did not specify. Do not leave a dev-only worst-case toggle in the PR unless asked.
6. **Self-review** for polish and motion before returning. Judge motion by feel: play it
   at 2 to 5 times its duration, step frame by frame, look for double-exposed colours,
   the wrong transform origin, properties drifting out of sync. Gestures need a real
   device; say so.

If you cannot capture the local render, say the comparison was by values and give the
user the URL to check by eye.

## Motion and polish

**Third-party motion skills are the starting understanding; the output is always code.**
Never return a motion plan or audit instead of code. The user judges motion by running it.

Read at the source, every time there is motion. Third-party skills are installed with
`npx skills add` (for example `npx skills add emilkowalski/skill`), pinned in
`skills-lock.json`, refreshed with `npx skills update -p`.

| Skill | When | Why |
|---|---|---|
| your taste skill (path in `CLAUDE.md`) | **always** | the user's judgment. Where it disagrees with a third-party skill, **it wins** in their own context. |
| `motion-*` (this harness) | always, if any exist | rules learned from the user's feedback. They outrank generic ones. |
| a polish skill (example: `emil-design-eng`) | always | the bar for component details and animation decisions |
| an animation decision skill (example: `animate`) | building any motion | should it animate, purpose, properties, curve, interruption, exit |
| a worst-case data skill (example: `break-ui`) | step 5 of the loop | finds the states Figma skipped |
| a mobile skill (example: `mobile-native`) | anything opened on a phone | viewport units, tap highlight, input zoom, safe areas |
| a motion review skill (example: `review-animations`) | self-review before returning | fix what it flags or say why not |
| a motion vocabulary skill (example: `animation-vocabulary`) | writing motion notes | gives feedback its exact name |

In a work context with a design system, the system decides, not the user's personal
taste. Motion the system cannot express becomes a handoff finding, not a workaround.

### Where the user's taste overrides third-party skills

Empty until real disagreements arrive. When a build or a refinement pass finds one,
the orchestrator adds a row. Never invent a row from assumption; each one must come from
the user's taste skill or a correction they made.

| Topic | Third-party default | The user's rule | Source |
|---|---|---|---|
| | | | |

### Growing motion rules from feedback

1. The engineer reports each motion correction under **Motion notes**: what it was
   (named with the vocabulary skill, or marked approximate), how often it is seen, its
   purpose, what the user changed it to, why, and whether it agrees or disagrees with
   the third-party polish skill. Disagreements are the most valuable.
2. The orchestrator writes it to memory as `taste` with `occurrences`.
3. At 3 occurrences, or when the user asks, the orchestrator writes it into
   `.claude/skills/motion-<topic>/SKILL.md` with the rule, the why and working code.
4. Publishing it into the user's own public skill repo is a separate step, only when asked.

## The PR is the handoff

For a work target the PR description is the developer's handoff. Structure it so an
engineer can lift the prototype without a meeting:

```
## What this is
One paragraph: the problem, who it is for, the Figma link, the preview link.

## Decided in the prototype
- <decision> · <why> · <what was rejected>

## Built with the design system
| Element | Component | Props that matter | Notes |

## Standalone components
| Component | Why the system did not cover it | Candidate for the system? | Path |

## States
| State | Covered | How it looks |
(empty, first-run, loading, error, permission, one item, many, longest string)

## Data shape
The mock data's shape, and which real entity it stands for.

## Deviations from Figma
| Where | Figma | Built | Why |

## How to check it
- Commands: exact and copy-paste.
- By eye: the screens and states to open, and what each should look like.
- Motion: what to watch at slow speed, and what reduced motion should do.
- Not verified here: what needs a real device or a person.

## Not done / open
What a developer must decide, and who to ask.
```

Plain words, short sentences, no em dashes. Personal-repo PRs use a short version: what,
why, how to check.

## Rules

- **Code only.** Never edit a Figma file from this agent.
- **Never invent a component or a prop.** Look it up.
- **Never push, open a PR, create a repo or deploy without the user's go** for this build.
- **Work information never goes into a personal repo.** See the wall in `context-intake`.
