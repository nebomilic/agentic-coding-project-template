# Product requirements

What we are building, and why. Owned by the Product Manager.

## Index

| # | Title | Status | Updated |
|---|---|---|---|
| [0001](0001-example-capability.md) | Example capability | Draft | <YYYY-MM-DD> |

Statuses: **Draft** → **Ready** → **In progress** → **Shipped** / **Dropped**.

## What a PRD contains

The problem, who has it, what success looks like, and what is explicitly out of
scope. It should be readable by someone who joined last week.

The success criteria do double duty: they are also where both automated and
manual acceptance checks come from (see
[ADR-0002](../adr/0002-testing-strategy.md)). Write them specifically enough
that someone could verify one without asking you what you meant. A criterion
nobody can trace a check back to will not be tested, and a check nobody can
trace to a criterion cannot be argued with when it fails.

## What a PRD must not contain

A solution. No frameworks, no databases, no protocols, no schema. If the
document specifies *how*, the technical decision has been made in the wrong
place, by the wrong owner, with no ADR recording it — and it will be discovered
months later when someone asks why.

The useful test: could two competent teams read this and build it with
completely different technology? If not, it has drifted.

Design links are the subtle case. A mockup is a specific visual solution, so a
PRD full of them quietly becomes a design spec with a problem statement
stapled to the front. For anything that establishes a pattern, link to a
`docs/design/` entry and let that entry hold the reference — one place to
update when the design moves, and the Designer owns the pointer to their own
work. Linking directly is fine for a genuine one-off screen.

## Before a PRD is marked Ready

- The Designer has reviewed the flows.
- The Developer has reviewed it for feasibility and scope realism.
- Out-of-scope is written down. Unstated scope expands silently.
