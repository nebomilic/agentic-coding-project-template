# Agent instructions — web application

Inherits the root `AGENTS.md`. Rules below take precedence within this folder.

## Boundaries

- This app consumes the API's public interface. Do not reach into the API's
  internals, replicate its database access, or duplicate its validation logic
  as the sole enforcement point.
- Do not add dependencies without checking whether `packages/shared` already
  provides the capability.
- Business rules that matter must be enforced server-side. Client-side checks
  are for user experience, not for correctness.

## Interface rules — owned by the Designer

These are not stylistic preferences. Violating them creates visible drift that
is expensive to unwind later.

- **Never introduce a colour, spacing value, font size, or radius outside the
  design tokens** in `packages/shared/tokens/`. If the design calls for a value
  that does not exist, stop and ask — do not hard-code it.
- **Every view handles four states**: loading, empty, error, and content. A
  view that only handles content is incomplete, regardless of whether the task
  mentioned the others.
- **Follow the established component patterns.** Before building a new
  component, check whether an existing one covers the case. A near-duplicate
  with slightly different behaviour is worse than reusing an imperfect fit.
- **Accessibility is a baseline, not a feature**: semantic structure, keyboard
  reachability, visible focus, meaningful labels on interactive elements, and
  text contrast that meets the standard recorded in `docs/design/`.
- **Copy is product-owned.** Do not invent user-facing text beyond obvious
  placeholders. Flag it for the Product Manager instead.

## Conventions

- <Naming conventions for files, components, modules.>
- <State and data-fetching conventions.>
- <Folder layout within this app.>

## Definition of done, this app

In addition to the root checklist:

1. Build passes and the linter reports no new warnings.
2. All four view states are handled.
3. No raw design values — tokens only.
4. The change works at the supported viewport range and with keyboard only.
5. Behaviour is tested through what the user does — rendered output and
   interaction — not through component internals or implementation detail. The
   non-content states carry behaviour too; an error state with a recovery
   action is logic, not decoration.
6. Anything left to a human check — visual judgement, motion, a real assistive
   technology — is named in the change description so it is a decision rather
   than an omission.
