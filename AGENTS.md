# Agent instructions — repository root

These are the baseline rules for any AI coding agent working in this
repository. They apply everywhere unless a nearer `AGENTS.md` overrides them.

## How to read this repository

1. **Nearest file wins.** If you are working in `apps/web/`, the instructions
   in `apps/web/AGENTS.md` take precedence over this file for anything they
   address. This file still governs everything they leave unsaid.
2. **Start with the README.** Before changing a folder, read its `README.md`
   for purpose and context. This file tells you the constraints; the README
   tells you the intent.
3. **Check the decision log.** `docs/adr/README.md` lists which technical
   questions are already answered. Do not re-decide them silently.

## Scope boundaries

- Change only what the task requires. Unrelated refactors, dependency bumps,
  and formatting sweeps belong in their own change.
- Do not create new top-level folders. The structure in the root `README.md`
  is deliberate; if the work genuinely does not fit, stop and say so.
- Do not move code between `apps/` and `packages/` as a side effect of another
  task. That is an architectural change and needs an ADR.
- Treat anything in `docs/adr/` with status `accepted` as a constraint, not a
  suggestion.

## When to stop and ask

Stop and surface the question rather than deciding yourself when:

- The task requires a technical choice that is not already covered by an ADR
  and would be costly to reverse.
- The task implies a product behaviour that is not described in any PRD.
- Implementing the request as written would contradict an accepted ADR.
- A user-visible decision is hiding inside a technical one. "Cache for 24
  hours" is technical; "users may see data that is a day old" is a product
  decision in technical clothing. The second needs a human.

## Writing documents

- **PRD** (`docs/prd/`) — you may draft one on request, never on your own
  initiative. PRDs describe problem and outcome only. If your draft names a
  framework, a database, or a protocol, it has drifted into ADR territory.
- **ADR** (`docs/adr/`) — write one whenever you make a technical decision
  that future work would have to live with. Use `docs/adr/TEMPLATE.md`. Number
  sequentially with four digits. Never edit an accepted ADR; write a new one
  that supersedes it and update the index.
- **Design** (`docs/design/`) — do not author these. Read them and follow
  them.

## Conventions that apply everywhere

- Filenames in `docs/` are zero-padded and kebab-case:
  `0007-short-descriptive-title.md`.
- Every document starts with a single `#` heading matching its subject.
- Prefer prose over bullet fragments in documents meant for humans; prefer
  explicit constraints over narrative in documents meant for agents.
- Code comments explain why, not what. If a comment restates the line below
  it, delete the comment.
- Never commit secrets, credentials, tokens, or real customer data — including
  in test fixtures, example configs, and documentation examples. Use obvious
  placeholders.

## Definition of done

Before reporting a task complete:

1. The change builds and the app's own checks pass (see the app's `AGENTS.md`).
2. Tests covering the changed behaviour exist and pass.
3. Any decision made along the way is recorded as an ADR.
4. Documentation that the change makes untrue has been updated in the same
   change.
5. You can state in one sentence what changed and why.

If any of these cannot be satisfied, say so explicitly rather than reporting
success.
