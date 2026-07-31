# snapshots.md - snapshot registry

The living registry of the template's snapshot directories: how to adopt one, who has. Unlike
the frozen snapshot artifacts it describes, this file is amended over time; the adopting
repo's agent adds its entry at adoption. Design rationale and provenance for each snapshot
stay in its proposal's `-notes.md` file; this file holds only usage and status.

## AGENTS-vc-x1-f5-20260803-snapshot

Status: proposed baseline, awaiting iiac-perf's review; not yet an adoption base.

Pin set: `AGENTS.md`, `CLAUDE.md`, `agent-data/` (now including `cycle-protocol.md` and
`versioning.md`, moved in from `notes/` so the pin-set boundary is the directory boundary).
The 20260802 set plus: the two protocol files pinned, cycle.md renamed cycle-checklists.md
(role-stating name beside cycle-protocol.md), jj.md's Revsets primer and long-lived bookmark
discipline, cycle-protocol.md's no-preflight review rule, jj-tips.md rehomed to a single
template-root copy. Provenance, the deliberate drop-list from iiac-perf's copy, and
the review asks are in [the notes](AGENTS-vc-x1-f5-20260803-notes.md); three-repo evidence in
[pin-set-dedup-review-20260803.md](pin-set-dedup-review-20260803.md).

The `work/` payload already tracks this baseline (restructured 2026-08-03, dogfood-first),
so repos inited before convergence get the proposed set; review amendments propagate to the
payload as they land. At convergence: amend this directory in place per the review (it is a
proposal, not an adopted base, so in-place amendment destroys no adoption record), flip its
status to active, and iiac-perf syncs (its adoption is coupled to its binary upgrade; see the
notes).

### Who is using

- vc-x1: adopted 2026-08-03 at 0.78.1, dogfood-first ahead of iiac-perf's review; re-syncs if
  the review amends the baseline
- iiac-perf: review pending (mailbox, 2026-08-03)

## AGENTS-vc-x1-f5-20260802-snapshot

Status: active adoption base.

Pin set: `AGENTS.md`, `CLAUDE.md`, `agent-data/`. These are the universal files a repo copies
verbatim and must keep byte-identical to its adoption base; `custom.md` is deliberately
outside the set. This line is the set's one definition, for adopters and for a future
`vc-x1 validate-agents` to check.

The 20260730 snapshot plus the 2026-08-02 graduation of dogfooded conventions (write to the
full width, cycle bookend titles, the checklist's close-the-records step, the mailbox check at
acquaint, plus two doc-consistency fixes in prose.md). Provenance and the per-amendment
sources are in [the notes](AGENTS-vc-x1-f5-20260802-notes.md). Cut as a new directory rather
than an in-place amendment: the template repo carries no commits yet, so amending in place
would have destroyed the record of what the cohort adopted.

Pending sync to iiac-perf: authored while iiac-perf had no session in flight but without its
review; see [its mailbox](../messages/iiac-perf.md). Remove this paragraph when its sync
lands.

### How to use

1. Copy the directory's contents (the pin set, defined above) to the adopting repo's root.
2. Verify the copies are byte-identical to the snapshot (`diff -r`); they stay verbatim, with
   every local change going to `custom.md` instead.
3. Write the repo's own `custom.md`, three `##` sections: "Medium and validation", "Project
   conventions and overrides", "Dogfood log". vc-x1's and iiac-perf's files are the worked
   examples.
4. Record the adoption as a dated entry in that `custom.md` dogfood log, citing this snapshot
   directory by name.
5. Add the repo to "Who is using" below.
6. Distill the repo's pre-restructure local conventions into `custom.md`; anything that looks
   universal is proposed into the template instead.

### Who is using

- vc-x1: adopted 2026-08-02 at 0.78.0-9, recorded in its custom.md dogfood log
- iiac-perf: pending (mailbox message 2026-08-02)
- zc-ring-x1: planned

## AGENTS-vc-x1-f5-20260730-snapshot

Status: superseded by 20260802; frozen.

The complete universal file-set of the 2026-07-30 AGENTS restructure proposal
([AGENTS-vc-x1-f5-20260730.md](AGENTS-vc-x1-f5-20260730.md)), as amended 2026-07-31 (rule 0,
hard-rules-first, generic pin lines, chores as-built ladder, chores Table of Contents);
artifact facts in
[the notes](AGENTS-vc-x1-f5-20260730-notes.md#the-snapshot-directory-added-2026-07-31).
The 2026-07-31 pending sync to vc-x1 was satisfied 2026-08-02 (vc-x1 synced to this snapshot's
content on its way to 20260802).

### Who used

- iiac-perf: adopted 2026-07-31, recorded in its custom.md dogfood log; 20260802 sync pending
- vc-x1: adopted 2026-07-30 at 0.78.0-1 (pre-amendment content); synced to the amended set
  2026-08-02 en route to 20260802
