# Agent instructions — shared package

Inherits the root `AGENTS.md`. Rules below take precedence within this folder.

## Hard constraints

- **Never import from `apps/`.** The dependency direction is one way, always.
- **Keep everything here pure.** No network calls, no filesystem access, no
  reading environment configuration, no assumptions about which runtime this
  executes in. Anything with a side effect belongs in an app.
- **Do not add code here because it has no obvious home.** If it is used by one
  app, it belongs in that app. If it fits nowhere, stop and say so — that is a
  structural question for a human.
- **Do not change design token values.** They are Designer-owned. You may add a
  token when a design explicitly calls for one and the value is specified; you
  may not invent a value to make something look right.
- **Changing an export is a breaking change.** Check every consumer in the
  repository before altering or removing one.

## Expectations

- Every exported function has a test, including its edge cases. This code runs
  everywhere; a defect here is a defect in every app simultaneously.
- Exports are deliberate. Internal helpers stay internal.
- New additions are documented in the package README when they change what the
  package is for.
