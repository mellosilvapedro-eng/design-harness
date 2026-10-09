---
name: skill-refinement
description: How this harness improves its own skills and agents. Mining methods from installed third-party skills and keeping only what the user's feedback in memory supports. Load before /design:refine-skills, and whenever a retro surfaces feedback about how an agent works.
---

# skill-refinement

The harness's skills get better one way only: **the user's feedback decides.**
Third-party skills are a supply of methods; memory is the filter. A method nothing in
memory supports is at most a trial. A method that contradicts the user's feedback or
taste skill is rejected, however good its author is.

## What can be changed

| Can change | Never change |
|---|---|
| this harness's skills (`design-*`, `context-intake`, `research-synthesis`, `skill-refinement`) and agents (`.claude/agents/`) | third-party skills installed by `npx skills add`, pinned in `skills-lock.json` |
| new local skills, for example `.claude/skills/motion-<topic>/` | the user's own taste or published skills, unless they ask |
| | design system skills or docs vendored in another repo |

## The pass

1. **Read the authority.** Everything in `memory/feedback/`, `memory/taste/`,
   `memory/patterns/`, `memory/critiques/`, `memory/you/growth.md`, and the open or
   rejected items in `projects/*/decisions.md` (repeated open items are feedback too).
   Then the user's taste skill. Then `memory/decisions/skill-refinements.md`, so nothing
   already rejected is proposed again.
2. **Mine the supply.** Dispatch one read-only agent over the third-party skills to list
   **methods** the harness lacks (process, checklists, review order, verification,
   severity calibration) and every place they disagree with the user's taste, with
   exact quotes. Aesthetic values (curves, durations, colours) are not candidates; those
   come from the taste skill.
3. **Filter each candidate:**

   | Verdict | When |
   |---|---|
   | **adopt** | a memory shows the failure it would have prevented, or a correction it matches |
   | **adopt, modified** | memory supports the idea but changes its shape |
   | **trial** | fills a real gap, contradicts nothing, no memory backs it yet |
   | **reject** | contradicts feedback, taste, or a harness rule |

   Memory alone can produce a change: a gap that stayed open across a project is a
   candidate with no third-party source.
4. **Edit in place**, in the target file's voice and length. One rule, one place. Plain
   words. Rewrite the method in two or three sentences; never paste a section in.
5. **Log every verdict** in `memory/decisions/skill-refinements.md` (with an index
   line): what changed, where, the source, the memory that justified it, and each
   rejection with its reason.

## Trials

A trial is promoted after three pieces of work without the user correcting it. If they
correct it once, remove it and log why. Unused is not failed.

## Taste disagreements

When a third-party skill disagrees with the user's taste, the user wins in their own
context and the design system wins in a system context. Record each in the
disagreements table in `design-engineering`. Never settle one by editing the user's
taste skill; tell them and let them decide.

## When to run

- After `/design:retro` notes feedback about how an agent works.
- After `npx skills update -p` pulls new versions.
- When the user asks.
