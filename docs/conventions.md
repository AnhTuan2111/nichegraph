# Engineering conventions

Adapted from the conventions of [second-bite](https://github.com/kl3inIT/second-bite/blob/main/docs/conventions.md) and
[hypomnema](https://github.com/kl3inIT/hypomnema/blob/main/AGENTS.md), both by kl3inIT, read on 18 November 2026.
Rules about code layout, errors, logging and tests are added with the first code, from the references chosen then.

## Change design

- Prefer the smallest complete path over scaffolding for a hypothetical future.
- Add no interface, adapter, configuration mode or package without a current caller. No empty package, no
  single-implementation interface.
- Use a clean cutover: migrate every caller and remove obsolete code, configuration, comments and tests in the same
  change.

## Reference-based design

- Before building a mechanism, look for it in the standard library, the installed libraries and well-maintained
  libraries. Take the option that meets the requirement with the least code left to own.
- When a reference implementation is the baseline, read it, cite its revision and code path, and separate observed
  behavior from inferred rationale.
- Before departing from the references, write down the requirement, what the references do, the proposed difference,
  its benefit, its cost and the simpler baseline. If the benefit does not justify the cost, keep the baseline.
- Carry accepted decisions across sessions. Do not reopen a rejected option or silently promote a suggestion into scope.

## Accounts and sources

- The tool reads only what the user's own account can already see, at a pace a person could keep. It does not post,
  react, follow or send messages.
- Cookies, session files and browser profiles stay on the user's machine, outside the repository.
- Posts are fetched to answer one question. What is kept afterwards, and for how long, is a decision recorded in an ADR
  before any storage is built.

## Documentation

- One canonical home per fact; link instead of copying.
- `ARCHITECTURE.md` states what exists, `docs/vision.md` the intent, ADRs the accepted rationale, `docs/research/` what
  was studied.
- A folder is created with its first document.
- Repository documents are written in English. A source kept as received stays in its own language.
