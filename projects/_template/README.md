Copy this folder to `projects/<slug>/` when starting a project.

`project.md` is the only required file. It is how the orchestrator resolves domain,
context, surface and phase in the next session. The rest appear as the work reaches them:

| File | Phase | Holds |
|---|---|---|
| `context.md` | 0 Context | what sources already say: decided, open, constraints, people |
| `brief.md` | 0 Frame | problem, who for, what changes if solved, how we would know |
| `research.md` | 1 Understand | evidence, what exists, what the data does and does not prove |
| `directions.md` | 2 Explore | references and the 2 to 4 directions considered |
| `decisions.md` | 3 Make | what was chosen, what was rejected, why |
| `critique.md` | 4 Critique | findings by severity, and what was done about each |
| `handoff.md` | 5 Handoff | states, edge cases, spec, copy |

Agents may write raw notes to `_raw/`, which is git-ignored. Phase 6 (Learn) writes to
`memory/`, not here.
