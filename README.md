# <Project Name>

> One sentence: what this product does, and for whom.

## What this repository is

This is the single repository for <Project Name>. It holds the product itself
(the applications and the code they share), the reasoning behind it (product
requirements, architecture decisions, design foundations), and the operating
instructions that both people and AI coding agents read before they change
anything.

The guiding idea: **code, intent, and decisions live together.** A change to
how the product behaves and the document explaining why it behaves that way
travel in the same pull request. Nothing important lives only in a chat
thread, a ticket comment, or someone's head.

## Repository map

| Path | What lives here | Owner |
|---|---|---|
| `apps/` | Deployable applications, one folder each | Developer |
| `packages/` | Code shared across apps, including design tokens | Developer |
| `docs/prd/` | Product requirements — what we are building and why | Product Manager |
| `docs/adr/` | Architecture decisions — technical choices and their consequences | Developer |
| `docs/design/` | Design foundations and cross-cutting UI decisions | Designer |
| `docs/runbooks/` | Operational procedures for when something needs doing or fixing | Developer |
| `infra/` | Environment and deployment definitions | Developer |
| `scripts/` | Repository-wide automation | Developer |
| `AGENTS.md` | Instructions for AI coding agents working in this repo | Developer |
| `CODEOWNERS` | Who must review changes to which paths | Shared |

## Getting started

1. Read this file.
2. Read `CONTRIBUTING.md` — it explains how work moves through the repo and
   who decides what.
3. Read the `README.md` of the app or package you are working in.
4. Skim `docs/adr/README.md` to see which technical decisions are already
   settled. Re-opening a settled decision is fine; doing it by accident is not.

Setup and run instructions are deliberately **not** here. They live in each
app's own README, because they differ per app and go stale fastest.

## The two-file convention

Every meaningful folder carries up to two documents, and they do different jobs:

- **`README.md` — for humans.** What this thing is, why it exists, how to run
  it, how it fits into the whole.
- **`AGENTS.md` — for AI agents.** Constraints, conventions, boundaries, and
  the checks that must pass before work is considered done.

They must not restate each other. When an agent needs context, `AGENTS.md`
links to the README rather than copying it. Duplicated prose is how one of
them quietly becomes wrong.

## Document lifecycle, in one line each

- **PRD** — written before the work, describes the problem and the desired
  outcome, never names a technology.
- **ADR** — written when a technical decision is made, immutable once
  accepted, superseded rather than edited.
- **Design doc** — written when a visual or interaction rule applies beyond a
  single screen.
- **Runbook** — written the second time someone has to figure out the same
  procedure.

## Status

<Current phase, e.g. "Pre-launch — v1 scope frozen, see docs/prd/README.md">
