# ADR-0001: Record architecture decisions

- **Status:** Accepted
- **Date:** <YYYY-MM-DD>
- **Deciders:** <names>
- **Related:** —

## Context

Technical decisions were being made in conversations, pull request comments and
chat threads. Within weeks the reasoning was gone, and only the outcome
remained. New contributors could see *what* the system did but not *why*, so
settled questions were re-opened, and constraints that had been chosen
deliberately looked like accidents.

AI coding agents sharpened the problem. An agent reads the current state of the
repository and reasons from it. Without a record of what was already decided
and why, it will propose a reasonable-looking change that quietly contradicts a
choice made for reasons it cannot see.

## Decision

We will record every architecture decision of consequence as a numbered
Markdown document in `docs/adr/`, following the template in this folder.
Accepted records are immutable; a changed decision is recorded as a new ADR
that supersedes the previous one.

## Alternatives considered

| Option | Why not |
|---|---|
| An external wiki | Drifts from the code, needs separate access, not visible to agents reading the repository |
| Comments in the code | Scattered, lost in refactors, no room for rejected alternatives |
| No formal record | The status quo that produced the problem |
| Editing records in place as decisions change | Destroys the history, which is the reason for keeping them |

## Consequences

**What this makes easier**

- The reasoning behind the system survives the people who made it.
- Agents can be pointed at a single folder to learn the standing constraints.
- Disagreements about settled questions become short: read the record first.

**What this makes harder, or commits us to**

- A small ongoing cost on every decision of consequence.
- An index that must be maintained, and a cadence to keep it honest — an
  out-of-date decision log is worse than none, because it is trusted.

**User-visible effects** — none.

## Revisit when

The log stops being read, or the cadence lapses for more than a quarter. At
that point the practice has already failed and should be fixed or dropped
deliberately rather than left to decay.
