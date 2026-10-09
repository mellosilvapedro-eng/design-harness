---
description: First run. Interview the user, fill the placeholders, and verify which sources are connected
---

Run the setup in `SETUP.md`, section "For the agent running setup". Read it in full
first and follow its three parts in order: interview, write, verify.

- Ask a few questions at a time, conversationally.
- Load `design-memory` before writing any memory file. Every new file gets an index line.
- Write only inside this folder.
- Every connector check is one **read-only** call. Never post, edit or create.
- Do not write a coordinate you could not verify. Flag what did not resolve.

If setup ran before, read the current `CLAUDE.md`, `contexts/` and `memory/sources/`
first, ask only about what is missing or changed, and leave the rest.

Finish with the customisation checklist from `SETUP.md`, ticked or not, and what the
user should connect next.
