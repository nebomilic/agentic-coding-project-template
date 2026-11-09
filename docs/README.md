# Documentation

Four kinds of document live here, each answering a different question and each
with a different owner.

| Folder | Question it answers | Owner | Lifecycle |
|---|---|---|---|
| `prd/` | What are we building, and why? | Product Manager | Living — updated as scope changes |
| `adr/` | Why is it built this way? | Developer | Immutable — superseded, never edited |
| `design/` | How should it look and behave? | Designer | Living — versioned by decision |
| `runbooks/` | How do we operate it? | Developer | Living — corrected after every use |

## The distinction that matters most

A **PRD** describes a problem and a desired outcome. An **ADR** describes a
technical choice and what it commits us to. The moment a PRD names a
technology, or an ADR decides something a user would notice, the document and
its owner have come apart. Both are common; both are worth catching in review.

## What is not here

Work state — what is in flight, who owns it, what is next — is deliberately
outside the repository, in the issue tracker.
[ADR-0003](./adr/0003-work-tracking.md) sets out why, and why a task list in
version control is the worst available option.

## Numbering

Documents in `prd/`, `adr/` and `design/` are numbered sequentially with four
digits and a kebab-case title:

```
0001-record-architecture-decisions.md
0014-move-session-state-server-side.md
```

Zero-padding keeps files sorting correctly past the ninety-ninth document. The
number is permanent once assigned — never reused, never renumbered, even if the
document is withdrawn.

## Index files

Each folder's `README.md` is its index. An index that is not updated in the
same change as the document is an index that lies, and a lying index is worse
than none: both people and agents will trust it.
