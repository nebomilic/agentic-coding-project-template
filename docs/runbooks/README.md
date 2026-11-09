# Runbooks

Operational procedures: how to do the things that have to be done to a running
system. Owned by the Developer.

## Index

| Procedure | When it is used | Last verified |
|---|---|---|
| <…> | <…> | <YYYY-MM-DD> |

## When to write one

The second time someone works out the same procedure from first principles. The
first time is discovery; the second is a signal that the knowledge is stuck in
one person's head.

## What makes a runbook usable

It will be read by someone tired, under pressure, who did not write it and may
not know the system well. That shapes everything:

- Lead with how to tell whether this is the right runbook.
- Numbered, literal steps. No implied knowledge, no "obviously".
- State what each step should produce, so the reader knows when it went wrong.
- Put the rollback at the end, written as carefully as the procedure itself.
- Include the escalation path and who owns the system.

## Keeping them true

A runbook is corrected **during** the next use, not after — the correction
never happens afterwards. Record a verification date in the index; an unverified
procedure older than a few months should be assumed wrong until someone walks
it.
