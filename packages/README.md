# Packages

Code used by more than one application.

## When something belongs here

Move code here when a **second** app needs it — not in anticipation of the
second app. Premature extraction produces abstractions shaped by a single use
case, which then have to be unpicked.

## Rules

- **Packages do not depend on apps.** The dependency direction is one way. A
  package that knows about an app is an app in the wrong folder.
- **Packages may depend on other packages**, provided the graph stays acyclic.
- **Each package has one clear responsibility**, stated in the first line of
  its README. If that line needs an "and", consider splitting it.
- **A package's public surface is deliberate.** Export what consumers need, not
  everything that exists.

## On `shared/`

`shared/` is the one package permitted a broad name, and it is the one most
likely to decay into a dumping ground. Its README states explicitly what
qualifies and what does not. Enforce that in review — the failure mode is
gradual and nobody notices until it is the largest thing in the repository.
