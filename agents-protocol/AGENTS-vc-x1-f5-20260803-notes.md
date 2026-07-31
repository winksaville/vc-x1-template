# AGENTS-vc-x1-f5-20260803-notes.md - provenance for the 20260803 baseline

What the 20260803 snapshot changes relative to 20260802, and why. Authored 2026-08-03 by
vc-x1's agent at wink's direction as a **baseline from vc-x1's perspective**: iiac-perf
reviews and refines, and the amended directory becomes the adoption base at convergence
(the 0730 proposal-review-adopt pattern). The three-repo evidence is
[pin-set-dedup-review-20260803.md](pin-set-dedup-review-20260803.md).

## Changes vs 20260802

- **Pin set grows by two files**: `notes/cycle-protocol.md` and `notes/versioning.md` move
  into `agent-data/`, so the pin-set boundary is the directory boundary and
  `diff -r agent-data/` catches all protocol drift. The `notes/` directory becomes records
  only.
  - cycle-protocol.md: vc-x1's copy is the base (trapezoid recipe, ladder-form chores, the
    0802 amendments), plus the changes below
  - versioning.md: vc-x1's copy, the only one carrying the 2026-07-30 "Grammar and storage"
    protocol (iiac-perf's and the payload's forked silently without it)
  - both gain the standard "Universal file, pinned..." header line
- **AGENTS.md file map**: the two files join the agent-data list; the records section is
  reworded to "records only, never universal rules".
- **cycle.md renamed cycle-checklists.md** (wink, at the 2026-08-03 adoption review): beside
  the newly pinned cycle-protocol.md the old name read as a scope collision; the new pair
  states the roles (act-time checklists vs full protocol with rationale and recovery). The
  files stay separate: hard rule 7's re-read-before-acting needs a file that is small and
  complete, and the protocol's recovery/rationale is exactly what act-time reads should skip.
  Only AGENTS.md linked the old name (five links, re-pointed).
- **jj.md gains two sections**:
  - "Revsets": the addressing primer condensed from jj-tips.md, so pinned files never link
    outside the pin set (cycle-protocol.md's `#revsets` links now target it)
  - "Long-lived bookmarks: merge-only by default, deletable once merged": the 2026-08-03
    refinement of "treated as permanent, never rebased"; evidence in vc-x1's custom.md
    dogfood log
- **cycle-protocol.md, beyond the move**:
  - "Reviewing changes" gains the no-preflight-while-a-review-iterates rule, salvaged from
    vc-x1's `notes/draft-reviews.md` (2026-04-28), which then deletes
  - links re-pointed: agent-data siblings flatten, `jj-tips.md#revsets` becomes
    `jj.md#revsets`
- **jj-tips.md leaves the per-repo payload**: one copy now lives at the template root
  (reference material, not protocol; its three per-repo copies had drifted).
- **The dogfood log moves out of custom.md into `notes/dogfood.md`** (wink, 2026-08-03): the
  log is a record (dated evidence, append-only), so under records-only it belongs in notes/,
  and custom.md loses its one section that could never converge. With the log out, matching
  the template's custom.md skeleton becomes custom.md's healthy steady state, and drift from
  the skeleton is a visible signal of project content accumulating. AGENTS.md's custom.md
  section and records list amended; the payload seeds `work/notes/dogfood.md` with the birth
  entry.

## What this baseline drops from iiac-perf's copy, deliberately

The baseline takes vc-x1's cycle-protocol.md, which describes the current (0.78.0, in-process
jj-lib) binary. iiac-perf's copy carries material tied to the older spawn-based binary it
still runs; the baseline drops it from the *pinned* file, not from existence:

- the "Merge non-ff recipe" (merge set up before the push): superseded by the trapezoid
  recipe, which reshapes between two pushes
- "Clear push's saved state" recovery (`.vc-x1/push-state.toml`, `--restart`): the in-process
  push keeps no saved state
- the 0.22.0 empty-commit post-mortem (vc-x1 push after a manual merge setup): tied to the
  old recipe; valuable history that belongs in iiac-perf's own notes/ as a project record if
  it wants to keep it visible

Adoption for iiac-perf is therefore coupled to the family binary upgrade already on the
tier-2 agenda; until it upgrades, its old-binary operational notes live in its custom.md or
notes/, not in the pinned set.

## Review asks for iiac-perf

- the two jj.md additions (revset primer wording, bookmark discipline)
- the drop-list above: anything the old-binary material covers that the baseline loses and
  should not
- the tier-2 items still open on your agenda (one-home, every-commit-belongs-to-a-cycle,
  scope-based version advancement): decide whether any land in this same snapshot before
  adoption
