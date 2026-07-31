# AGENTS-vc-x1-f5-20260802 notes

Provenance for `AGENTS-vc-x1-f5-20260802-snapshot/`, the first snapshot cut as a new directory
rather than an in-place amendment: the template repo carries no commits yet, so editing
`AGENTS-vc-x1-f5-20260730-snapshot/` in place would have destroyed the only record of what the
dogfood cohort adopted. The 20260730 snapshot is now frozen for real; this one is the active
adoption base.

Authored 2026-08-02 by vc-x1 (f5) + wink, in the template because it is the family's safe
cross-repo write point. Content: the 20260730 snapshot (with its 2026-07-31 amendments) plus
the first graduation of dogfooded custom.md conventions into the pinned set, from the
2026-08-02 vc-x1 close-out session following iiac-perf's `feat: dynamic warmup` trapezoid.

The amendments, and where each came from:

- **prose.md, Prose form: write to the full width.** Wrap near the <=100 limit instead of
  imitating legacy narrow text. A default, not an absolute. One fact per bullet or sub-bullet.
  Dogfooded as iiac-perf's custom.md convention (2026-08-02) and vc-x1's same-day adoption
  (chores-15 reflow, TODO.md, custom.md).
- **prose.md, Conventional-commit shape: cycle bookend titles.** Opening title = close-out
  title + " opening", same type, so one `git log --grep` returns the pair. Dogfooded at
  iiac-perf 0.24.0 (`feat: dynamic warmup opening` / `feat: dynamic warmup`) and retro-applied
  to vc-x1's `0.78.0-0` (`refactor: jj-lib migration opening`).
- **prose.md, Conventional-commit shape: the chores-surface bullet now describes the as-built
  ladder** instead of the `Commits: [[ref]]` line. Repairs a 2026-07-31 miss: the notes.md /
  cycle.md ladder amendment left this bullet contradicting them (found at vc-x1's 2026-08-02
  sync).
- **prose.md, Typeable punctuation only: the prohibition is on authoring, not presence.**
  Rewords the opening so the transcription exception below it no longer contradicts "Banned:".
  This is the wording that bounds any sweep (vc-x1 chores-15 "Why the source sweep left the
  ladder").
- **cycle.md, Per-commit checklist: new step 4 "Close the records"** (backfill previous push's
  refs, append the chores rung / TODO block, bump the version-of-record); old steps 4-8 become
  5-9. From iiac-perf's 2026-07-31 dogfood finding: given "desc and push", an agent following
  the checklist verbatim skipped all three.
- **AGENTS.md, Working practices: check the mailbox at acquaint.** Both repos carried the same
  custom.md entry verbatim, which is the signature of something universal; MESSAGES.md always
  said agents need it written into their instructions.

Deliberately not included (tier 2, pending iiac-perf's read): the one-home narrative
convention, promoting `notes/cycle-protocol.md` into the byte-identical set (the family's
copies currently disagree on the trapezoid recipe while pinned cycle.md links to
`#trapezoid-close-out-recipe`), and "every commit belongs to a cycle".
