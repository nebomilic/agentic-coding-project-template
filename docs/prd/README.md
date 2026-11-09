# Product requirements

What we are building, and why. Owned by the Product Manager.

## Index

| # | Title | Status | Updated |
|---|---|---|---|
| [0001](./0001-example-capability.md) | Example capability | Draft | <YYYY-MM-DD> |

Statuses: **Draft** → **Ready** → **In progress** → **Shipped** / **Dropped**.

## What a PRD contains

The problem, who has it, what success looks like, and what is explicitly out of
scope. It should be readable by someone who joined last week.

## What a PRD must not contain

A solution. No frameworks, no databases, no protocols, no schema. If the
document specifies *how*, the technical decision has been made in the wrong
place, by the wrong owner, with no ADR recording it — and it will be discovered
months later when someone asks why.

The useful test: could two competent teams read this and build it with
completely different technology? If not, it has drifted.

## Before a PRD is marked Ready

- The Designer has reviewed the flows.
- The Developer has reviewed it for feasibility and scope realism.
- Out-of-scope is written down. Unstated scope expands silently.
