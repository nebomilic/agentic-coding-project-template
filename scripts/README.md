# Scripts

Repository-wide automation: tasks that span apps or set up the repository
itself.

## What belongs here

- Repository setup and bootstrap.
- Cross-app checks run in CI.
- Maintenance and migration helpers used across the repository.

## What does not

Anything specific to one app. It belongs with that app, where its owner will
find it.

## Rules

- **Every script is safe to run twice.** A script that only works on a clean
  machine will be run on a dirty one, under pressure, by someone who did not
  write it.
- **Destructive scripts confirm before acting**, and state exactly what they
  are about to change.
- **Each script explains itself** — a short comment block at the top covering
  what it does, when to run it, and what it changes. A `--help` flag where the
  interface is not obvious.
- **No secrets, no credentials, no environment-specific values.** Read them
  from the environment.

## Index

| Script | Purpose |
|---|---|
| <…> | <…> |
