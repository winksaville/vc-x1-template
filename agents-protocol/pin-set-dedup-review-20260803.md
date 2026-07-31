# pin-set-dedup-review-20260803.md - three-repo protocol-file review

A 2026-08-03 review (vc-x1's agent, at wink's request) of protocol-file duplication across
vc-x1, iiac-perf, and this template's `work/` payload, plus one new convention proposed for
promotion. Input to the tier-2 discussion already on iiac-perf's agenda (mailbox message
2026-08-02); nothing here is decided until that review.

## Findings: where the copies stand

- **Pin set** (`AGENTS.md`, `CLAUDE.md`, `agent-data/`, per
  [snapshots.md](snapshots.md#agents-vc-x1-f5-20260802-snapshot)):
  - vc-x1 and `work/` are byte-identical to the 20260802 snapshot
  - iiac-perf is on the 0730 set (drifts on AGENTS.md, cycle.md, prose.md, exactly the 0802
    graduations); its sync request is already in its mailbox
- **`notes/cycle-protocol.md`**: three-way divergence, the largest in the family
  - vc-x1 (738 lines): trapezoid close-out recipe, ladder-form chores sections (the 0802
    amendments)
  - iiac-perf (702): the older "Merge non-ff recipe" and pre-0802 chores form
  - `work/` (649): older still (shorter merge recipe and pushing recovery)
  - already on the tier-2 agenda; the recipes disagree in mechanics, so unification needs
    iiac-perf's input
- **`notes/versioning.md`**: new finding, not on the agenda
  - vc-x1 carries the "Grammar and storage" section (the 2026-07-30 version protocol: one
    prose spelling, the single `-`, the PEP 440 `+` remap, identify-never-order)
  - iiac-perf and `work/` are byte-identical to each other and both lack that section, so the
    07-30 protocol never propagated
- **`notes/jj-tips.md`**: three near-copies of a generic jj tutorial (revset walkthroughs,
  terminal transcripts), not a project record
  - vc-x1 vs `work/`: 3-line link-target drift (agent-data/jj.md vs the pre-restructure
    AGENTS.md anchor)
  - iiac-perf: ~66 diff lines of older content
  - referenced by each repo's cycle-protocol.md (`#revsets`) and iiac-perf's README
- **The rest of each repo's `notes/`** (chores, done, backlog, plan and topic files): genuine
  project records, no cross-repo duplication, nothing to dedup.

## Proposal 1: the pin-set boundary is the directory boundary

The drift above all lives in files that are universal in intent but sit outside the pin set,
in `notes/`, beside project records that must never be pinned. Make the boundary structural:

- **`agent-data/` holds everything universal (pinned); `notes/` holds only project records.**
- `notes/cycle-protocol.md` moves to `agent-data/cycle-protocol.md` once its content is
  unified (both close-out recipes kept as named shapes, custom.md picking the default, which
  is how vc-x1's custom.md already words it).
- `notes/versioning.md` moves to `agent-data/versioning.md`, adopting vc-x1's copy (the only
  one with the 07-30 grammar).
- `notes/jj-tips.md` is reference material, not protocol: keep one copy hosted here in the
  template, drop the per-repo copies. The protocol-relevant revset primer folds into
  agent-data/jj.md so the pinned files never link outside the pin set. Alternative if the
  fold feels heavy: keep jj-tips.md in the `work/` payload but explicitly unpinned.
- AGENTS.md's file map and every `../notes/cycle-protocol.md` link re-point in the same
  change; `diff -r agent-data/` then catches all protocol drift in one command.

We think this is the structural fix for how versioning.md silently forked: a universal file
in `notes/` has no drift check, one in `agent-data/` does.

## Proposal 2: long-lived bookmark discipline (promote into agent-data/jj.md)

Refined 2026-08-03 in vc-x1 (custom.md convention + dogfood entry) after wink deleted the
fully merged `refactor-vc-x1@origin`; replaces the "treated as permanent (merge-only onto
main, never rebased)" wording. Proposed as a new jj.md section:

- long-lived bookmarks are merge-only by default: conflicts with `main` are resolved in merge
  commits, never by rewriting published rungs
- a rebase is never required for correctness; it is a linearity preference
- coordinated rebases stay available (the bar is on unilateral rewrites), at the known cost of
  staling git-SHA citations in the records; chids and ochid trailers survive a rebase
- once a bookmark's history is fully merged into `main` the bookmark is redundant and may be
  deleted

The evidence trail is vc-x1's custom.md dogfood log, 2026-08-03 entry.

## Sequencing

1. Baseline authored from vc-x1's perspective (done, 2026-08-03):
   [AGENTS-vc-x1-f5-20260803-snapshot/](AGENTS-vc-x1-f5-20260803-snapshot/), provenance and
   review asks in [the notes](AGENTS-vc-x1-f5-20260803-notes.md).
2. vc-x1 adopted the baseline 2026-08-03 at 0.78.1 (dogfood-first, the 0730 precedent),
   deleting its `notes/` copies of the moved files plus `draft-reviews.md` (salvaged into the
   protocol); the `work/` payload restructured to match the same day.
3. iiac-perf reviews the baseline plus the standing tier-2 agenda; amendments land in the
   snapshot directory in place (it is a proposal, not an adopted base), then propagate to the
   payload and vc-x1.
4. At convergence the snapshot's status flips to active and iiac-perf syncs, recording the
   adoption in its dogfood log (coupled to its binary upgrade; see the snapshot notes).
