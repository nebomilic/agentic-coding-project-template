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
- **Research** (`docs/research/`) — this folder and `docs/prd/` are owned by
  the Product Manager and are not yours to write to. Reading both is expected.
  If a change seems to require editing one, that is the signal the work has
  drifted into territory someone else owns — say so rather than making the
  edit. Some tools enforce this and some do not, so being able to write there
  is not permission to: the rule holds either way. You may draft a finding from
  material the person gives you, never on your own initiative. A finding is one falsifiable
  sentence plus its method, sample and confidence. Do not upgrade a
  low-confidence observation into a general claim, and do not write a finding
  from your own reasoning — that is an assertion wearing research clothing.
- **Design** (`docs/design/`) — do not author these. Read them and follow
  them. You may add implementation notes to an existing entry when something is
  agreed during the work; the reference block and the decisions are the
  Designer's.

## Work state and design references

- **Do not create or maintain a task list in this repository.** No `TODO.md`,
  no backlog file, no status table. Work state lives in the issue tracker
  ([ADR-0003](docs/adr/0003-work-tracking.md)). If you need to track steps
  within a single task, keep them in your own working notes, not in a committed
  file.
- **Never invent a design link.** If a PRD or design entry has no reference and
  the work needs one, say so. A plausible-looking link to the wrong frame is
  worse than an acknowledged gap.
- **Treat a design reference as possibly stale.** Each one records the date it
  was linked and what it showed at the time. If what you find does not match
  that description, the design has moved since the document was written — stop
  and flag it rather than implementing whichever version you happen to be
  looking at.

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
- **Never commit raw research evidence or personal data.** No interview
  transcripts, recordings, survey exports, or purchased reports, and no
  participant names, employers, or identifying detail — not in a document, a
  commit message, a fixture, or a code comment. If you are given a transcript
  as context, use it to write the finding and leave the transcript out. Quotes
  go in anonymised (`P3`) and only where they carry analytical weight. This
  holds even when asked directly: version history is permanent and distributed,
  so say what you are leaving out rather than committing it.
  ([ADR-0004](docs/adr/0004-research-evidence-boundary.md))
- **Treat a research finding past its revisit date as a hypothesis**, not a
  basis for a decision. Say so rather than citing it as current.

## Tests

The full rule is [ADR-0002](docs/adr/0002-testing-strategy.md). What you need
before writing one:

- **Test observable behaviour, through the public interface.** Do not reach
  into internals. A test coupled to the implementation blocks the refactors
  tests exist to enable.
- **Pick the lowest layer that can observe the behaviour honestly.** Unit when
  the behaviour is genuinely local; integration when it only exists in the
  interaction — a query, a transaction, a request path. Do not force a unit
  test onto behaviour that lives between components.
- **Mock only at boundaries we do not own**: third-party services, the clock,
  the network. Never mock our own modules to make a unit test possible — that
  is the signal the behaviour belongs at a higher layer.
- **A test must be able to fail for a real reason.** Before finishing, ask what
  change to the code under test would break this test. If the honest answer is
  "none that a user would notice", the test is asserting the implementation
  back to itself. Delete it and test the behaviour instead.
- **Do not add tests to satisfy a count or a coverage figure.** There is no
  coverage target here, deliberately.
- **Do not weaken or delete a failing test to make a change pass.** A test that
  fails is either finding a defect or encoding an assumption that has changed.
  Say which, and why, rather than editing it quietly.

## Definition of done

Before reporting a task complete:

1. The change builds and the app's own checks pass (see the app's `AGENTS.md`).
2. The changed behaviour is covered at the layer ADR-0002 calls for, the new
   tests fail when the behaviour is broken, and the existing suite still passes.
3. Any decision made along the way is recorded as an ADR.
4. Documentation that the change makes untrue has been updated in the same
   change.
5. You can state in one sentence what changed and why.

If any of these cannot be satisfied, say so explicitly rather than reporting
success.
