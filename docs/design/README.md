# Design

Visual and interaction decisions that apply beyond a single screen. Owned by
the Designer.

## Index

| # | Title | Status | Updated |
|---|---|---|---|
| [0001](./0001-design-foundations.md) | Design foundations | Current | <YYYY-MM-DD> |

## Source of truth

**The design tool remains canonical for visuals.** Nothing here tries to mirror
screen designs; that duplication would be stale within a sprint.

Canonical file: <link>

What lives here instead are the decisions that a mockup cannot carry:

- **Foundations** — the token system, and the reasoning behind its scales.
- **Rules that span screens** — state conventions, density, motion, hierarchy.
- **Accessibility baseline** — the standard we hold to and what that means in
  practice.
- **Component policy** — when to reuse, when to extend, when a new component is
  justified.
- **Which design file is canonical**, and what to do when it and the
  implementation disagree.

## Why these must be written down

A decision that exists only as a comment in a design file is invisible to a
developer six months from now and invisible to every coding agent working in
this repository. The implementation will drift from it, and the drift will only
surface when someone notices two screens disagree. Writing the rule down, and
encoding its values in `packages/shared/tokens/`, is what makes it enforceable.

## Relationship to tokens

Documents here explain *why* the system is shaped as it is.
`packages/shared/tokens/` holds the values themselves, and is what the code
consumes. When the two disagree, the tokens are what ships — so a change to the
reasoning is incomplete until the tokens follow.
