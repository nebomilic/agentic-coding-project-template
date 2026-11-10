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
| Work item state | — lives outside the repo, see [ADR-0003](docs/adr/0003-work-tracking.md) | — | — |

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
[ADR-0004](docs/adr/0004-research-evidence-boundary.md).

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

**What this does not cover.** Three gaps, in order of how often they matter:

- **Other tools.** This file is read by Claude Code. An agent reaching the
  repository another way — a desktop session with the folder connected, for
  instance — is not bound by it and can write anywhere in the tree. Verified,
  not assumed. For those, `AGENTS.md` is the only layer carrying the boundary,
  which is a reason to keep it short enough to actually be read.
- **Shell commands.** `sed -i`, `mv`, `tee` are probably not caught even in
  Claude Code.
- **Determined effort.** This is a guardrail against the accidental write, not
  a wall.

`git diff` remains the thing that catches what slips through all three.

**Verifying it loaded.** A malformed rule is skipped with a warning rather than
failing loudly, so a typo gets you silent non-enforcement. `claude doctor`
lists rejected entries; `/status` shows which setting sources are active.

## How this is worked

Four systems, each holding what it is actually good at. The repository is the
hub: it holds every durable claim, and the others hold the things a repository
handles badly.

| What | Where | Why not the repo |
|---|---|---|
| Decisions, requirements, findings, operating knowledge | **This repository** | — |
| What is in flight, who owns it, what is next | **Issue tracker** | State changes a dozen times a week; version control turns that into commit noise and merge conflicts ([ADR-0003](docs/adr/0003-work-tracking.md)) |
| Visual designs | **Design tool** | Mirroring screens in text goes stale within a sprint; `docs/design/` holds the decisions and the references instead |
| Interview recordings, transcripts, purchased reports | **Wherever evidence lives** | Unreviewable in a diff, and personal data must not enter permanent distributed history ([ADR-0004](docs/adr/0004-research-evidence-boundary.md)) |

Links run one way: from the other systems **into** the repository. A ticket
points at a PRD; a PRD never restates a ticket. The moment a copy appears
somewhere else, the two begin drifting and nobody can tell which is current.

### Sessions

AI sessions split along the same line the ownership matrix does. Three, by
role rather than by task:

- **Product.** Research, synthesis, drafting PRDs and findings. Reads the
  codebase for context, never writes to it.
- **Development.** Implementing, tests, ADRs, git. Reads the PRD rather than
  being told what it says. `.claude/settings.json` blocks its writes to
  `docs/prd/` and `docs/research/`.
- **Review.** Fresh, pointed at a diff, with one question: does this
  contradict anything already accepted? Working alone, this is the substitute
  for the reviewer `CODEOWNERS` assumes — and it is better than re-reading
  your own work, because it cannot be anchored by remembering why you did it.

Splitting by task instead — a session per feature — puts two sessions in the
same files, and neither knows the other exists. Keep concurrent sessions in
disjoint parts of the tree; the second write wins silently.

### The handoff is files, not conversation

This is the discipline the whole arrangement rests on, and the one that slips
first. A PRD sitting uncommitted has not been handed off — the next session
reads whatever happens to be on disk, mid-edit.

Commit at the boundary, then switch. Sessions share no memory, so `git log` is
the only record of what each actually did.

### Obsidian

An editor and a navigator over the repository, not a part of it. It opens the
folder as it stands — no import, no conversion.

What it adds that a code editor does not: **backlinks**. Open a document and
the sidebar lists everything citing it. That is the blast radius, and it
matters most at the moment you are about to supersede an ADR or mark a finding
stale — those are exactly the moments you need to know who was relying on it.
An ADR with no backlinks at all is usually missing from its index.

Two rules keep it from becoming a dependency:

- **Markdown links, not wikilinks.** `[[0003-work-tracking]]` renders as
  literal text everywhere else and is invisible to agents. `.obsidian/app.json`
  is committed so this is set for anyone who opens the vault; the rest of
  `.obsidian/` is local and gitignored. Path form matters too — the full link
  convention is in [AGENTS.md](AGENTS.md).
- **No plugin-rendered content in committed documents.** A Dataview query
  standing in for the ADR index would be a code block to everyone not running
  Obsidian, and to every agent. The one exception is `docs/_dashboard.md`,
  which is entirely queries and is marked as a tool by its underscore prefix —
  nobody reads it expecting prose.

Open the vault at the repository root, not at `docs/`. The documentation spans
the tree — app and package READMEs are part of it.

**One plugin is required**, and only for the dashboard: **Dataview**. Without
it, `docs/_dashboard.md` shows its queries as plain code blocks and nothing
else breaks. Note that installing a community plugin does not enable it —
Settings → Community plugins, then the toggle beside it. An installed-but-off
plugin looks exactly like a broken file.

Optional and unrelated to the structure: **Obsidian Git** (commit without
leaving the editor, which matters because an uncommitted document has not been
handed off) and **Advanced Tables** (these documents are mostly tables, and
editing them by hand is miserable).

### Two things worth noticing

Both are the arrangement telling you something is wrong upstream:

- **You are explaining in the development session what the PRD should have
  said.** The PRD is underspecified. A single session carries that missing
  context in its head and never notices it is absent from the file.
- **A write to `docs/prd/` or `docs/research/` is refused.** The work has
  drifted into territory someone else owns. Say so rather than routing around
  it.

### What is still provisional

The roles, the boundaries and the handoff discipline are settled — they follow
from the ownership matrix and the ADRs. The specific tools are not. Replace any
of them without touching anything else; the constraint that matters is that
nothing committed depends on a particular one.

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

All three are walks through an index, asking of each row whether it is still
true. Done by hand that is slow enough to get skipped, which is the failure
this repository is least protected against.

If you use Obsidian, open `docs/_dashboard.md` — it shortens the walk with
queries for orphaned documents, oldest findings, and what depends on what.
Nothing to set up; it is a file in the repository. Improve a query and commit
it, and the next project inherits it.

It is a convenience, not a dependency. Without it the cadences still work, just
by hand, and the committed indexes remain the authority either way.

## Writing style

Documents are read under time pressure, often by someone new and increasingly
by a machine. Lead with the conclusion. State constraints as constraints. If a
paragraph could be deleted without losing information, delete it.
