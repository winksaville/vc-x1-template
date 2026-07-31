# Notes

This directory holds the project's records: chores, bugs, the long-tail backlog, and topic
files, each organized for easy reference. Records only; universal rules live in
`../agent-data/` (see [../AGENTS.md](../AGENTS.md)'s file map).

By default there are the chores-NN.md files in [chores/](chores). Chores are general notes
about tasks; short-term tasks and their status live at the repo root in
[../TODO.md](../TODO.md). The chores-NN files are numbered in sequence; the highest-numbered
file is the active one, older ones are closed.

Multi-cycle programs too big for a TODO.md entry get their own dated plan file here: one `##`
section per stage, so chores and todo entries can reference a stage by anchor. The plan file
owns the forward design; chores still records each shipped cycle.

A rule that governs what the artifact does, rather than a record of what was done, gets its
own topic file so it can be found without knowing which cycle produced it. The investigation
behind such a rule stays where it happened (a plan file or a chores section) and is linked
from the policy, so neither restates the other.

Example chores file:

```
# Chores-01.md

General maintenance tasks and considerations for the project see other files for
more specific topics. A chore in a chores file provides quick information on the
how and why of a particular chore.

## Create a binary that lists jj info

This binary should list the changeID, commitID, and description title
and using `jj-lib`
```

## Workflow and conventions

Bot-facing workflow and conventions live in [`../AGENTS.md`](../AGENTS.md) (hard rules + file
map) and its `../agent-data/` satellites:

- [Notes file conventions](../agent-data/notes.md): Todo format, Reference numbering, Notes
  references (`[[N]]` citation style), Markdown anchor links, Retiring Done entries, Chores
  conventions (section headers / Done entries exact-title rule, content rules, the as-built
  ladder and its commit reference format, the chores Table of Contents).
- [Prose and durable text](../agent-data/prose.md): prose form, typeable punctuation,
  conventional-commit shape.
- [Code conventions](../agent-data/code.md): doc comments, `// OK: ...` on `unwrap*` calls.
- [Cycle protocol](../agent-data/cycle-protocol.md) and its act-time
  [checklists](../agent-data/cycle-checklists.md): cycle shape and numbering, per-commit
  flow, commit descriptions, pushing and close-out shapes.
- [Versioning](../agent-data/versioning.md): the version scheme and the version-of-record.
