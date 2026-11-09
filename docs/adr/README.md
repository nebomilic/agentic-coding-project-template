# Architecture decisions

Why the system is built the way it is. Owned by the Developer.

An ADR records a decision that future work has to live with, the context that
made it reasonable, and what it commits us to. It is not documentation of how
the system works — that is what code and READMEs are for. It is a record of a
choice, kept so that nobody has to reconstruct the reasoning from the outcome.

## Index

| # | Title | Status | Date |
|---|---|---|---|
| [0001](./0001-record-architecture-decisions.md) | Record architecture decisions | Accepted | <YYYY-MM-DD> |
| [0002](./0002-testing-strategy.md) | Testing strategy | Accepted | 2026-11-09 |

Statuses: **Proposed** → **Accepted** → **Superseded by #NNNN** / **Deprecated**.

Keep the status column honest. Both people and agents read this table as the
current state of the world; an entry still marked Accepted six months after
reality moved on will be cited confidently and wrongly.

## When to write one

Write an ADR when the decision would be expensive to reverse, when it
constrains future work, or when a reasonable person might later ask "why on
earth is it like this?" — which is most decisions that take more than an
afternoon to argue about.

Do not write one for choices that are cheap to change. The log is valuable in
proportion to its signal.

## Rules

- **Accepted ADRs are immutable.** Do not edit the decision or the context. If
  the decision changes, write a new ADR that supersedes the old one, and update
  both entries in this index.
- **Supersession is a link in both directions.** The new ADR names what it
  replaces; the old one names what replaced it.
- **A decision with user-visible consequences needs the Product Manager's
  agreement**, recorded in the consequences section. "Cached for 24 hours" is
  technical; "users may see day-old data" is a product decision wearing
  technical clothing.
- **Numbers are permanent.** A rejected or withdrawn ADR keeps its number and
  stays in the folder. The gaps in a renumbered log are how history gets lost.

## Review cadence

The ADR index is reviewed every two weeks by all three roles, for fifteen
minutes. The only question is: is anything here no longer true?
