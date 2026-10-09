---
name: context-intake
description: The context connector. Which sources can tell us what a task is about (chat, docs, meeting transcripts, the inbox, local files), how to reach each one, how to tell work from personal, and the shape of the context pack that comes back. Load before dispatching context-curator, before /design:context, and when adding a context source.
---

# context-intake

Design work starts from what was already said somewhere: a thread, a spec, a meeting.
This skill:

1. says **which sources exist** and how to reach each (the adapters);
2. decides **which domain** a task belongs to, `work` or `personal`;
3. defines the **context pack** an agent returns.

## The domain axis

Context says *whose design language*. Domain says *whose information*, and so where it
may be searched and where it may flow. Fill the signals during setup.

| Signal | Domain |
|---|---|
| example: the employer's product, team, customers, metrics, channels, docs | `work` |
| example: the user's own site, side projects, published skills, anything under their name | `personal` |
| a talk, post or portfolio piece **about** work | `personal`, reading `work` sources; see the wall |
| unclear | **ask**, in one sentence, before searching |

Domain usually matches context, but not always. Resolve both; never infer one silently.

### The wall

Information crosses domains in one direction only, and only on purpose.

- **Work to personal is blocked by default.** Nothing from work sources goes into a
  personal repo, a public page or a published skill unless the user approved that exact
  use. Customer names, revenue, internal metrics, people's names and unreleased plans
  never cross, even when approved; summarise them out.
- **Personal to work is allowed** but named: "this comes from your own notes".
- A pack has one domain. Items from the other domain go in `Crossed`, not the pack.

## The adapters

Check the tool is actually present before reporting a source. Report each source's mode
in the pack's first line. Setup trims this table and sets the State column; a source is
`verified` only after a live read call returned real data, recorded in
`memory/sources/connectors.md`.

| Source | Reach it with | Domain | Good for | State |
|---|---|---|---|---|
| **Chat** (for example Slack) | the connector's search, read-thread and read-channel tools | set in setup | decisions in threads, who asked, status, objections | not verified |
| **Docs** (for example Notion) | the connector's search and fetch tools | set in setup | specs, RFCs, prior initiatives, guidelines | not verified |
| **Meeting transcripts** | your transcript tool's connector, or files in `inbox/` | tag per meeting | who wanted what, decisions, owners | not verified |
| **Inbox** | `Read`/`Write` on `inbox/`, filed by the curator | set when filing | anything the user hands over | always available |
| **Local** | `Read` on project folders, repos in `memory/sources/repos.md`, `memory/` | `personal` for own repos | prior decisions and projects | always available |

### Chat

Usually the highest-value work source.

- **Channels by default; direct messages only when asked**, and then only what bears on
  the task. Never quote a personal exchange.
- **Read the whole thread** behind any hit. A message without its replies is how a
  reversed decision gets reported as current.
- Record channel, date and link for every item used.

### Docs

Keyword search is often literal, not semantic: search 3 to 5 narrow terms. Workspaces
hold duplicates; prefer the most recently edited copy and say which you read.

### Transcripts

Weakest per sentence, strongest for *who wanted what*. Read for decisions, open
questions, owners and dates, not quotes. **Decided** is not the same as **said**.

**All sources are read-only.** Connectors may be able to send, react or edit. None of
that is used here, not even to ask a question. If someone needs asking, tell the user.

## Intake: the user hands it over, the curator files it

The user never works in folders. Whatever they give goes to the curator as-is.

**Handoff.** Subagents cannot see the chat, so the orchestrator writes anything pasted
**verbatim** to `inbox/_new/<YYYY-MM-DD>-<n>.md` and passes the path. File paths and
links pass as they are.

**Filing.** For each item the curator:

1. **Classifies the domain.** Unclear: leave it in `_new/` and return one question.
2. **Saves it** to `inbox/<domain>/<YYYY-MM-DD>-<slug>.md`, where the slug says what it
   is, with frontmatter:

   ```
   ---
   kind: transcript | thread | doc | note | file
   domain: work | personal
   source: pasted | <original path> | <url>
   date: <when it happened, or "unknown">
   project: <slug or none>
   people: [<names that appear>]
   ---
   ```

   A pasted item moves out of `_new/`. A file from elsewhere is **copied**, never moved.
   A link is saved as the link plus the parts that mattered.
3. **Uses it** in the pack, citing the inbox path.

Never delete or edit a filed item. If misfiled, move it and say so.

## The context pack

```
mode: chat <state> · docs <state> · transcripts <which> · inbox <n read, n filed>
domain: work | personal          context: <name> | ask
task: <one line, as understood>

## What this is about
3 to 5 lines: the problem as the sources describe it.

## Decided
- <decision> · <who>, <date> · <source link>

## Open
- <question or disagreement> · <who holds it> · <source link>

## Constraints
- <deadline, dependency, limit> · <source link>

## People
- <name> · <role in this task>

## Filed
- <inbox path> · <kind> · <domain> · from <pasted | path | url>, or "nothing new"

## Sources read
- <title> · <type> · <date> · <link or path> · <why it mattered>

## Crossed
- items from the other domain, held back, or "none"

## Gaps
- what we looked for and did not find, and where it probably is
```

- **Every claim carries a source and a date.** Undated means stale.
- **Newer beats older, decided beats said.** Show disagreements under `Open` with dates.
- **Never invent a decision from silence.**
- The orchestrator writes the pack to `projects/<slug>/context.md`.

## Adding a source

Add a row: how to reach it, domain, what it is good for, state `not verified`. Make one
read-only call, then update the state and `memory/sources/connectors.md`.
