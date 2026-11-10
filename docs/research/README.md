# Research

Findings that inform what we build. Owned by the Product Manager.

## Index

| # | Title | Confidence | As of | Revisit |
|---|---|---|---|---|
| [0001](0001-example-finding.md) | Example finding | Medium | <YYYY-MM-DD> | <YYYY-MM-DD> |

## Findings, not evidence

This folder holds **curated claims**: what we learned, how confident we are,
and what it rests on. It does not hold the raw material those claims came from
— interview transcripts, recordings, purchased reports, survey exports.

The distinction is not about importance. It is about what a repository is good
at. A finding is short, durable, reviewable in a diff, and useful to anyone who
reads it later. A transcript is long, raw, and reviewable only in the sense
that someone clicks approve. Merge a few of those and "merged means reviewed"
stops being true for the documents where it mattered.

Raw evidence lives wherever your team keeps it. Each note records where, so the
chain from claim back to source stays intact without the source being here.

See [ADR-0004](../adr/0004-research-evidence-boundary.md) for the full
reasoning, including the parts that are not negotiable.

## Perishability

Every other document here has a stable lifecycle. An ADR is immutable. A PRD is
living. A runbook is corrected when reality moves.

A research finding is **perishable**: true as of a date, decaying on its own
while nobody touches it. A competitor analysis from two years ago read as
current is the lying index again — except nothing flags it, because unlike an
ADR nobody ever supersedes a finding. It simply sits there, looking like a
fact.

So every note carries two dates. **As of** is when the finding was true.
**Revisit** is when to stop trusting it without checking. Past that date the
finding is a hypothesis, not a basis for a decision, and both people and agents
should treat it that way.

Review the index each planning cycle. A note past its revisit date is either
re-confirmed with a new as-of date, superseded by newer work, or marked stale.
Leaving it unmarked is the failure mode this section exists to prevent.

## Confidence

State it explicitly, because a reader cannot infer it from tone:

| Level | Means |
|---|---|
| High | Multiple independent sources, or a sample large enough to argue from |
| Medium | Consistent signal from a small sample, or one solid source |
| Low | Indicative only — one conversation, an impression, a single data point |

A low-confidence finding is still worth recording. An unlabelled one is worse
than nothing, because it gets cited as though it were high.

## Before you write a note

- The claim fits in one sentence. If it needs three, it is probably several
  findings.
- The method and sample are stated. "Users want X" from two conversations and
  from forty are different claims.
- Quotes are anonymised and load-bearing. A quote that only illustrates tone
  carries personal data for no analytical gain — cut it.
- The pointer to raw evidence names a location and an owner, not a bare link to
  something only one person can open.
