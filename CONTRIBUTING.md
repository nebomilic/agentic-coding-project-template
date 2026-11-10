# Contributing

How work moves through this repository, and who decides what.

## Roles

Three roles own this repository: **Product Manager**, **Developer**,
**Designer**. Ownership here means two separable things — who *writes* a
document, and who must *approve* a change to it. Conflating them is the most
common reason documentation rots: when everyone is vaguely responsible, nobody
is.

## Ownership matrix

| Artifact | Writes / decides | Contributes | Must approve |
|---|---|---|---|
| `docs/prd/*` | Product Manager | Designer (flows), Developer (feasibility) | Developer, on scope realism |
| `docs/adr/*` | Developer | Product Manager, where the decision has product cost | Developer lead |
| `docs/design/*` | Designer | Developer (feasibility) | Designer |
| `packages/shared/tokens/*` | Designer owns values, Developer owns format | — | Designer and Developer |
| Root `README.md` | Product Manager | Everyone | — |
| Root `AGENTS.md` | Developer | PM (domain language), Designer (UI rules) | Developer |
| `apps/*/AGENTS.md` | Developer of that app | Designer, for user-facing apps | Developer |
| `apps/*/README.md` | Developer of that app | — | — |
| `docs/runbooks/*` | Developer | Whoever operates the procedure | — |
| Application code | Developer | — | Developer |
| Automated tests | Developer | — | Developer |
| Acceptance criteria | Product Manager | Developer, Designer | Product Manager |
| Manual acceptance run | Whoever ships the change | — | — |
| Design references and versions | Designer | — | Designer |
| `docs/research/*` | Product Manager | Designer (user research) | Product Manager |
| Work item state | — lives outside the repo, see [ADR-0003](./docs/adr/0003-work-tracking.md) | — | — |

`CODEOWNERS` encodes this matrix as a mechanism. Keep the two in sync; if they
disagree, `CODEOWNERS` is what actually happens.

## Boundaries that are easy to blur

**A PRD must not specify a solution.** It answers *what* and *why*. The moment
it names a database, a framework, or a protocol, the decision has been made in
the wrong document, by the wrong owner, without the ADR trail. Catch this in
review.

**An ADR must not make product decisions.** Technical choices with user-visible
consequences need the Product Manager's agreement, recorded in the ADR's
consequences section. The test: if a user would notice, it is not purely
technical.

**Acceptance criteria are product-owned, test layers are developer-owned.**
The Product Manager states what must be true for the work to count, as success
criteria in the PRD. The Developer decides how that is verified and at which
layer. Neither does the other's half: a PRD prescribing test types has crossed
into implementation, and a suite with no traceable criteria is verifying
whatever the developer assumed.

**Research findings belong here; research evidence does not.** A curated
finding — one claim, its method, its confidence — is reviewable and durable.
A transcript is neither, and carries personal data into permanent, distributed
history. The boundary is not negotiable for anything involving a person; see
[ADR-0004](./docs/adr/0004-research-evidence-boundary.md).

**Design decisions must reach the repository.** The design tool remains the
source of truth for visuals, and nothing here tries to mirror it. But rules
that apply beyond a single screen — spacing scale, state conventions,
accessibility baseline — must exist as text in `docs/design/` and as values in
`packages/shared/tokens/`. A decision that lives only in a design-tool comment
is invisible to both new developers and coding agents, and the implementation
will drift from it.

## Enforcing ownership at write time

`CODEOWNERS` routes review when a change is proposed. `.claude/settings.json`
is the other half: it stops an agent writing to paths it does not own in the
first place.

```json
"deny": [
  "Edit(/docs/prd/**)",
  "Edit(/docs/research/**)"
]
```

Reads stay open — a session implementing a feature must be able to read the
PRD and the research behind it. Only writing is blocked.

**Why these two paths and not `docs/**`.** The list is deliberately short, and
widening it breaks things:

- **`docs/adr/` must stay writable.** `AGENTS.md` instructs whoever is doing
  the work to record decisions as ADRs. Denying it would put the rules in
  conflict with each other.
- **`docs/design/` cannot be expressed at path level.** Implementation notes
  may be added to an existing entry; the reference block and the decisions may
  not. That is section-level ownership, finer than any file path can reach, so
  it stays enforced by instruction.

More generally: a rule that blocks legitimate work gets resolved by deleting
the file, and then nothing is enforced at all. Add a path only after something
has actually gone wrong.

**What this does not cover.** Shell commands — `sed -i`, `mv`, `tee` — are
probably not caught. This is a guardrail against the accidental write, not a
wall. `git diff` remains the thing that catches what slips through.

**Verifying it loaded.** A malformed rule is skipped with a warning rather than
failing loudly, so a typo gets you silent non-enforcement. `claude doctor`
lists rejected entries; `/status` shows which setting sources are active.

## Workflow

1. **Problem is framed.** PM writes or updates a PRD. Designer and Developer
   review it for flow and feasibility before it is marked ready.
2. **Approach is chosen.** Developer records any decision that future work must
   live with as an ADR. Small, reversible choices do not need one — the test is
   whether reversing it later would be expensive.
3. **Work happens.** Changes stay scoped. Documentation that the change makes
   untrue is updated in the same pull request, not a follow-up.
4. **Review.** `CODEOWNERS` routes the review automatically. Reviewers check
   the boundaries above, not only the code.

## Cadence

- **Decision review, every two weeks, fifteen minutes, all three roles.** Walk
  the ADR index. Mark anything that reality has overtaken as superseded. Skip
  this and the index will be lying to you within a quarter — and agents will
  confidently cite decisions you reversed months ago.
- **PRD index review, each planning cycle.** Close what shipped, drop what will
  not happen.
- **Research index review, each planning cycle.** Anything past its revisit
  date is re-confirmed, superseded, or marked stale. Nothing enforces this, and
  an unmarked expired finding gets cited as fact.

## Writing style

Documents are read under time pressure, often by someone new and increasingly
by a machine. Lead with the conclusion. State constraints as constraints. If a
paragraph could be deleted without losing information, delete it.
