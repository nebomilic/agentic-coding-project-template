# Review dashboard

A tool, not a document — the underscore prefix marks it as such. Open it in
Obsidian for the review cadences in `CONTRIBUTING.md`.

It is committed so it travels with the repository, but it is the one file here
that does not read well outside Obsidian: the queries below are inert code
blocks anywhere else, including to an agent reading the raw file. That is the
trade for having it at all. Nothing here is authoritative — the index files
are; these queries only tell you where to look.

> Requires the **Dataview** community plugin, enabled (installing is not
> enabling).

---

## Works today

These query the file tree and the link graph, which exist regardless of how
metadata is written.

### Orphans — documents nothing links to

An ADR nothing references is usually a sign something went wrong: a decision
recorded and then never cited, or an index entry that was missed.

```dataview
LIST
FROM "docs"
WHERE length(file.inlinks) = 0
  AND file.name != "README"
  AND file.name != "TEMPLATE"
  AND file.name != "_dashboard"
SORT file.folder ASC, file.name ASC
```

### Research, oldest first

A crude staleness proxy until frontmatter exists — last-modified rather than
as-of, so it will mislead on a file you touched for a typo. Treat it as a
prompt to look, not as an answer.

```dataview
TABLE file.mtime AS "Last touched", length(file.inlinks) AS "Cited by"
FROM "docs/research"
WHERE file.name != "README" AND file.name != "TEMPLATE"
SORT file.mtime ASC
```

### Blast radius — what depends on a document

Change the folder to point at whichever document you are about to supersede,
or just open the file and read its backlinks pane. This version lists every
research finding with its dependents.

```dataview
TABLE length(file.inlinks) AS "Dependents", file.inlinks AS "Cited by"
FROM "docs/research" OR "docs/adr"
WHERE file.name != "README" AND file.name != "TEMPLATE"
SORT length(file.inlinks) DESC
```

### Everything, by folder

```dataview
TABLE WITHOUT ID file.link AS "Document", file.folder AS "Folder"
FROM "docs"
WHERE file.name != "_dashboard"
SORT file.folder ASC, file.name ASC
```

---

## Needs YAML frontmatter

These do not work yet. Our templates put metadata in bold lists
(`- **Status:** Accepted`), which Dataview cannot read. Switching the templates
to YAML frontmatter would unlock them.

That switch is a real change to every document and has a cost — slightly less
pleasant to read raw — so it is worth making only once you know you want these
queries. If you do make it, the fields would be `status`, `as_of`,
`revisit_by`, `confidence`, `owner`.

### Expired research findings

The query that would most directly fix the weakest part of the structure —
a finding past its revisit date is a hypothesis, and right now nothing says so.

```dataview
TABLE confidence, as_of, revisit_by
FROM "docs/research"
WHERE revisit_by != null AND revisit_by < date(today)
SORT revisit_by ASC
```

### ADRs still marked Accepted

Not a problem in itself — just the list to walk fortnightly, asking of each:
is this still true?

```dataview
TABLE status, deciders
FROM "docs/adr"
WHERE status = "Accepted"
SORT file.name ASC
```

### PRDs in flight

```dataview
TABLE status, updated
FROM "docs/prd"
WHERE status != "Shipped" AND status != "Dropped"
SORT status ASC
```

---

## What no query can check

The part that needs a person, and the reason the cadence is a meeting rather
than a dashboard:

- **Is the ADR index honest?** A status column can say `Accepted` and be
  wrong. Only someone who knows what changed can tell.
- **Does a finding still hold?** The revisit date says when to ask, not what
  the answer is.
- **Has a design moved since the PRD was written?** Open the reference, read
  the state-at-link-time line, compare with what you see. Nothing automates
  this.
- **Is scope still what we said?** Shipped work drifts from its PRD quietly.
