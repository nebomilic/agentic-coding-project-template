# ADR-0003: Work tracking and the state layer

- **Status:** Accepted
- **Date:** 2026-11-09
- **Deciders:** <names>
- **Related:** [ADR-0001](0001-record-architecture-decisions.md)

## Context

With requirements in `docs/prd/`, technical decisions in `docs/adr/` and
operating knowledge in `docs/runbooks/`, the knowledge a tracker used to hold
now lives in the repository — reviewed, diffable, and readable by agents
without a connector.

That raises the obvious question: is a tracker still needed at all?

The question conflates two jobs trackers do, which have little to do with each
other. They store knowledge, and they run a state machine. Trackers were always
poor at the first: a ticket description is written once, read during
implementation and never curated, with no review gate, no supersession and no
maintained index. Nobody opens a three-year-old ticket to understand why the
system is as it is. Moving that knowledge into the repository fixes a problem
trackers were already failing at.

The second job is different, and the repository is actively bad at it. Our
documents are built on a horizon test: does this still matter in a month? A work
item's state is the opposite — a dozen transitions in a week, none individually
meaningful. Held in version control it produces commit history dominated by
status noise, textual merge conflicts over semantically uncontested
reorderings, no concurrent editing, no notification on change, and a state that
becomes branch-dependent and therefore incoherent.

## Decision

We will keep durable knowledge in the repository and work state outside it, in
the smallest tool that can hold the state.

1. **Tickets carry no knowledge.** A work item holds an identifier, a state, an
   owner, and a link into the repository. The description is not a restatement
   of a PRD; the duplicate is what we are eliminating.
2. **No task list in version control.** Specifically no `TODO.md`, no backlog
   file, no status table an agent maintains. That arrangement gets the commit
   noise and the merge conflicts without gaining views or notifications, while
   diluting the signal in the artifact store.
3. **Prefer the forge's own issues** — the issue tracker attached to the
   repository — over a separate product, while work is repo-scoped. It is
   adjacent to the code without being in the file tree.
4. **A separate tracker earns its place** when work spans repositories, when it
   is not code at all, when it has intake from outside the team, or when
   non-technical participants need a front door that is not a pull request.
   Then it holds state only, and every description links into the repository.

## Alternatives considered

| Option | Why not |
|---|---|
| Keep full tickets with descriptions | Reinstates the duplicate: a worse copy of the PRD, drifting from the moment it is written |
| Markdown task files in the repository | Commit noise, merge conflicts on ordered lists, branch-dependent state, no notifications |
| A full tracker regardless of team size | Pure overhead for repo-scoped work, and a second place for knowledge to rot |
| Abolish tracking entirely | Loses the one thing trackers do well: current state, ownership, and who is told when it changes |

## Consequences

**What this makes easier**

- Agents get standing context ambiently from the repository rather than through
  a connector that may not be queried.
- One source for every durable claim, with review and history behind it.
- Tickets become cheap to write and cheap to close, because they hold almost
  nothing.

**What this makes harder, or commits us to**

- Two systems to keep in step. The discipline is that the link always points
  from the ticket into the repository, never the reverse, and never a copy.
- Work that is not code has no home here, and will need somewhere when it
  arrives.
- Nothing notifies the repository when something outside it changes — including
  a design moving after the PRD was written (see `docs/design/README.md`).

**User-visible effects** — none.

## Revisit when

Work routinely spans repositories, non-code work becomes a significant share,
or external intake starts arriving through the wrong door. Also revisit if
tickets start growing descriptions again — that is the duplicate returning, and
it means the link into the repository is not being trusted.
