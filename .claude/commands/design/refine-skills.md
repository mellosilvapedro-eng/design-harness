---
description: Improve this harness's own skills and agents from installed third-party skills, filtered by the user's feedback in memory
argument-hint: [optional focus, e.g. "critique", "motion", "after skills update"]
---

Refine skills. Focus: **$ARGUMENTS**

Load `skill-refinement` and `design-memory`.

1. Read the authority: feedback, taste, patterns, critiques, `memory/you/growth.md`, open
   and rejected items in `projects/*/decisions.md`, and
   `memory/decisions/skill-refinements.md` so nothing rejected is proposed again.
2. Dispatch one read-only agent to mine the installed third-party skills for methods and
   taste disagreements, with exact quotes.
3. Filter every candidate: adopt, adopt modified, trial or reject, each with the memory
   that decided it.
4. Edit the harness skills and agents in place. Never edit third-party skills or the
   user's own taste skill.
5. Log every verdict in `memory/decisions/skill-refinements.md`, with an index line.
6. Tell the user in a few lines what changed, what was rejected because of their
   feedback, and any taste disagreement they should decide.
