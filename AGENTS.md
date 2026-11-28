# NicheGraph repository guide

## Where to look

- What exists today: [ARCHITECTURE.md](ARCHITECTURE.md). Facts only, updated in the change that makes them true.
- Goal, principles and the questions still open: [docs/vision.md](docs/vision.md). Intent, not fact.
- Engineering rules: [docs/conventions.md](docs/conventions.md).
- What was studied, with sources: [docs/research/](docs/research/README.md). Reference clones live in `.tmp/` (git-ignored).
- Why a decision was made: [docs/decisions/](docs/decisions/README.md).
- Work and progress: GitHub issues on the repository, once it is published. There is no roadmap file.

## Talking to the owner

- Answer in Vietnamese with full diacritics, short, in plain words. Lead with the answer. Keep technical terms in
  English.
- Give one recommendation with its reason, not a survey. Ask one question at a time, and make it stand on its own:
  what it is about, what is there now, why it is asked, what each option leads to.
- Never use a bare internal identifier: say what it is ("issue #3, the Threads source").
- Separate what was read in code or docs from what is inferred; mark the second as such.

## Act or ask

- **Ask first** before: writing code for a design that has not been approved; anything outward-facing, shared or hard
  to undo (creating the GitHub repository, pushing, opening or merging a pull request, deleting, spending money);
  logging in to or automating a social account; choosing between designs; widening the scope of an issue.
- **Act without asking** on: anything the owner approved in this conversation and its obvious follow-ups (tests,
  fixing CI, updating docs); reading, searching and cloning references into `.tmp/`.
- When in doubt about scope, do the smaller thing and say what was left out.

## Working rules

- Research before design: study mature open-source projects from primary sources (code, official docs), compare,
  recommend one, then wait ([reference-based design](docs/conventions.md#reference-based-design)).
- Do not invent logic. Every decision, in a design, an issue or a reply to the owner, says which reference it is
  learned from ("From", "Học từ"). Logic no reference has is left out unless the owner asked for it; then the line
  names the owner and the date.
- When comparing options, the amount of code to write is not a cost: agents write it. Weigh complexity instead:
  moving parts, failure modes, what has to be operated, and how hard the result is to understand and change.
- Documents are leads, not proof. Before designing or fixing on what a document says, check it against the code on
  `main` or the running program and cite what you saw (a path and line, a command and its output).
- Every code change has a GitHub issue holding its design and plan; a change that spans several days or adds a
  component gets its design approved in the issue before code. Branch `<issue>-<slug>`, commit subjects
  `type(scope): summary (#<issue>)`, one pull request per issue, merged with a merge commit (not squashed) once CI is
  green and the owner has approved it.
- Issue titles are `type(scope): summary`; a pull request takes its issue's title with ` (#<issue>)` added, as
  hypomnema's pull requests do (owner, 2026-11-28). `type` is one of `feat`, `fix`, `docs`, `chore`, `refactor`,
  `test`, `ci`; `scope` is the part touched (`run`, `source`, `runtime`, `store`, `web`, `skill`, `ci`, later `hub`)
  and is left out when a change touches several; `summary` is English, starts in lower case, says what the change
  makes, and stays within 72 characters. A design that spans several pull requests is one issue, and each pull
  request has its own issue marked "Part of #<design issue>".
- Any change to the interface or how it is used is drawn in Figma first, with the components already in the Figma
  file; the app keeps that one set of components (owner, 2026-11-28).
- Docs-only changes (`docs/`, `AGENTS.md`, `README.md`) go straight to `main` with the subject `docs: summary`, after
  the owner has read them.
- Commits carry the owner's name only: no co-author or "generated with" lines.
- Never write a secret to Git, documents, issues, logs or command history: API keys, passwords, cookies, session
  tokens, browser profiles. Record only where a secret is managed.
- Write repository documents in English and update them in the change that makes them true. One fact has one home;
  link instead of repeating.
- Record an ADR only after the decision is accepted and implementation has started. ADRs are append-only; supersede
  one with a new ADR.
