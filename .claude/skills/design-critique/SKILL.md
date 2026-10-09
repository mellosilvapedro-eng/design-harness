---
name: design-critique
description: How to critique a design. The order to look in, severity levels, and how to write a finding that can be acted on. Load before any design critique, peer review or self-review, whether the artefact is a Figma file, a live URL, a prototype or code.
---

# design-critique

Critique judges **design**: whether it solves the problem, whether it holds together,
where it breaks. It is not lint. If a CI gate or linter would catch it, say so in one
line and move on.

## Look in this order

The order keeps you at the right altitude. A beautiful screen that answers the wrong
question is not a craft problem.

1. **Does it solve the stated problem?** Read the brief. If not, that is the finding.
2. **Flow and structure.** Intent to done; arriving from somewhere unexpected; going
   back; undo. On every screen: where am I, where can I go, what is here, how do I get out.
3. **Hierarchy.** What does the eye hit first? More than one primary means none wins.
4. **States.** Empty, first-run, loading, partial, error, permission-denied, one item,
   a thousand items, longest plausible string, a language that breaks the layout. List
   every value the screen shows, where it comes from, its limit and whether it can be
   missing; test at the real limit. A field with no limit is a finding. Check nothing
   hides under fixed chrome on the last row.
5. **Content.** Do labels say what happens? Does the error say what to do next?
6. **Consistency across the project.** Do totals match their rows? Is the same thing
   named the same everywhere? Did a typo survive from an earlier version?
7. **System fidelity.** Real components and tokens, or lookalikes? Is anything built on
   an experimental component?
8. **Craft.** Spacing rhythm, alignment, optical centring, type scale, motion that
   confirms rather than performs.
9. **Accessibility.** Contrast on the real background, target size, focus order
   and visibility, keyboard path, reduced motion, meaning carried by colour alone.
10. **Edges.** Narrow and wide viewports, dense data, both themes. For code: the real
    container width, 320px, the widest layout, 200% zoom. Say which you saw rendered.

## Severity

| Level | Means | Test |
|---|---|---|
| **blocker** | ships broken, or solves the wrong problem | someone hits it on a normal path and cannot proceed |
| **major** | works, but costs real users or trust | you would argue to delay a release |
| **minor** | clear improvement, clear fix | worth doing before handoff |
| **nit** | preference, below the noise floor | you would not say it twice |

**Frequency moves severity.** Friction on a screen used many times a day outranks the
same friction on a settings page. Say the frequency when it changed the grade.

Tag **fragile** when it works today but is one realistic step from breaking.

Rank most severe first. **Cap at about 8 to 12 findings**; the rest is a count. If
nothing is wrong, say so.

## Writing a finding

> **[major] Bulk actions have no undo** · table toolbar, selected state
> Destructive by default with no reversal. A mis-click on a 200-row selection is
> unrecoverable, and the confirm does not say how many rows are affected.
> **Fix:** state the count in the confirm ("Archive 47 items?") and add an undo toast.

- **What and where**: component, frame or file:line.
- **Why**: the principle from the **active context's** language, named. When it is your
  own judgement, say "general judgement". Never a vague "best practice".
- **The fix**: concrete and smallest first: remove, reduce, correct, then polish. Change
  only what the finding is about.

## The verdict comes first

Open with one line: **ship**, **ship after the blockers**, or **rethink**, and the finding
that decided it.

## Never

- **Describe what you cannot see.** Write "not verifiable from a static render".
- **Restyle to your own preference.**
- **Stack findings on one root cause.** One finding, several consequences.
- **Soften a blocker.**
- **Report a finding you have not re-checked.** Go back to each one; confirm it exists,
  is not a recorded decision, and is not a reading artefact (an unloaded page reads as empty).
- **Re-open a settled decision** without new evidence.

## When it is the user's own work

Same standard. The orchestrator tallies the **kind** of each finding into
`memory/you/growth.md`. Mark recurrences: "third time empty states were missing" beats
the finding alone.

## Peer review

Add **what is working and why**, and keep **broken** separate from **arguable**.
