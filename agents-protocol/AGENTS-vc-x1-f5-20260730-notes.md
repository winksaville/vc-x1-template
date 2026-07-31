# AGENTS restructure proposal: companion notes

Companion to [AGENTS-vc-x1-f5-20260730.md](AGENTS-vc-x1-f5-20260730.md), the proposed universal
AGENTS.md. That file is the draft as it would ship; this file is everything that shouldn't ship
with it: the problem, the design reasoning, the satellite inventory, the dogfood plan, and the
open questions other agents should weigh in on.

Authored 2026-07-30 by Claude (Fable 5) working in the vc-x1 repo, with Wink. Frozen as a
discussion snapshot; the live copy evolves in vc-x1 during its 0.78.0 cycle (see
[Dogfood plan](#dogfood-plan)).

## The problem

Two halves, maintenance and adherence.

**Maintenance: there is no shared core anymore.** Measured 2026-07-30 against vc-x1's AGENTS.md
(871 lines), by changed lines of `diff`:

- `vc-x1-work-repo-template/AGENTS-vc-x1.md`: 19
- `vc-x1-work-repo-template/AGENTS.md`: 429
- `iiac-perf/AGENTS.md`: 442
- `zc-ring-x1/AGENTS.md`: 582

Four ~700-870-line forks; a rule fix learned in one repo never propagates, because nothing
marks which lines are universal and which are project-local.

**Adherence: recall at the moment of action, not disagreement.** The rules that get broken in
practice (pre-committing a rung, the hard stop after push, dropped ochid trailers, title
identity, punctuation) are procedural constraints spread across ~1,800 always-relevant lines
(AGENTS.md + cycle-protocol.md + satellites), written as narrative-with-rationale. We think the
failure mode is: at decision time the agent needs the imperative, extracting it from prose
under a full working context is where slips happen, and everything always-loaded competes with
the task for attention. The redesign therefore optimizes for two distinct readers: the agent
about to act (needs a short checklist it can re-read in full) and the agent asking why (needs
the rationale). Today one document serves both and serves the first badly.

## The design

- **A short universal `AGENTS.md`** (~150 lines): the dual-repo model, a numbered hard-rules
  list (the moment-of-action invariants, each with a pointer to its detail), condensed working
  practices, and a file map. The numbering lets a review name a rule ("that violates hard
  rule 3").
- **`agent-data/` satellites**, universal, read at the moment of action rather than always
  loaded: `cycle.md` (the checklists), `jj.md`, `prose.md`, `notes.md`, `code.md`. Checklists
  sit at the top of their file, rationale after: rule first, why second, inverting the old
  order.
- **`custom.md`**, one per repo, the only agent-editable instruction file: the medium's
  validation commands, versioning specifics, project-local overrides (an override names the
  section it supersedes), and a dogfood log. Loaded last, wins conflicts. `CLAUDE.md` becomes
  `@AGENTS.md` + `@custom.md`.
- **Pinning as the enforcement mechanism.** Every instruction file except `custom.md` must
  match the template byte-for-byte, so drift is detectable with `diff` (and a future
  `vc-x1 validate-agents` could check it). The "custom.md is the only editable file" contract
  is then checkable for free: any edit outside it shows up as template drift.
- **The full cycle protocol stays in `notes/cycle-protocol.md`** (v1 decision, revisitable):
  `agent-data/cycle.md` carries the checklists and defers to the protocol on any disagreement.
  This bounds the restructure diff and keeps the protocol's recovery procedures where existing
  links point.
- **Semantics-preserving v1.** Rules keep their current meaning; only the organization changes.
  We think that keeps any adherence change attributable to the structure, which is the
  hypothesis under test; semantic rule changes become dogfood findings, not v1 edits.

## Satellite inventory

Full text lives in vc-x1's `agent-data/` during the dogfood window (this snapshot carries only
the main file). Contents:

- **cycle.md** (new text; the protocol remains authoritative):
  - The cycle at a glance; Committing vs pushing (moved from AGENTS.md).
  - Per-commit checklist (the 8-step flow, condensed).
  - Ladder (sub-cycle) checklist.
  - Before any push; After the final push: hard stop.
  - Close-out checklist; vc-x1 push behaviors.
- **jj.md** (moved from AGENTS.md): jj basics; ochid trailers; re-describing (coordinate
  first, keep the trailer); resolvability; `.vc-config.toml`.
- **prose.md** (moved): prose form; problem + plan shape; semicolons inside bullets; typeable
  punctuation only; conventional-commit shape; speculation marker; plain synopsis.
- **notes.md** (moved): read-the-slice; notes references; reference numbering; markdown anchor
  links; todo format; retiring Done entries; chores conventions (all three subsections).
- **code.md** (moved): line width; doc comments everywhere; `// OK: ...` on `unwrap*` calls.

The per-commit checklist, as the sample of the checklist form (its numbered steps condense
cycle-protocol.md's Per-commit flow):

1. Mark the rung `(current)` in `TODO.md > ## In Progress`, as the first edit.
2. Do the work. On any deviation from the agreed plan, or any question, stop and surface it.
3. Flip `(current)` -> `(done)`, before validation and the commit.
4. Validate the artifact (commands in custom.md). Skip-able for notes-only commits, mandatory
   at close-out.
5. Say "ready to commit" and stop; the user reviews the working-copy diff.
6. Write the description (<=72-col conventional title; body file-by-file, opening with the
   version-bump bullet).
7. Show title + body and stop for review. This covers the push only when the user's go
   explicitly includes it.
8. On the user's go: `vc-x1 push <bookmark> --title "..." --body "..."`. Never pre-commit with
   `jj commit`; never hand-write `ochid:` trailers.

## Dogfood plan

Adopted in vc-x1 at `0.78.0-1 docs: adopt universal AGENTS`, so the rest of that cycle (a docs
rung, two refactor rungs, a feat rung, a fix rung, and a trapezoid close-out) runs under the
new files.

- **Authority flips during the window**: vc-x1's local copy is the working draft and is
  amended freely; this snapshot is frozen. Promotion back to the template (en masse or
  incremental) is when the flow reverses and pinning switches on.
- **Amendments are the data**: small fixes ride as riders on whatever rung is in flight, big
  ones get their own docs rung; every one gets a dated line in custom.md's dogfood log. The
  log is the evidence for the promotion decision.
- **Template per-project forks retire at promotion**: `AGENTS-vc-x1.md` /
  `AGENTS-iiac-perf.md` style copies become each repo's `custom.md`; the discussion-snapshot
  naming (`AGENTS-<repo>-<model>-<date>.md`) stays for proposals like this one.

## Migration sketch (other repos, at promotion)

1. Copy `AGENTS.md` + `agent-data/` from the template.
2. Distill the repo's current AGENTS.md deltas into its `custom.md` (medium, validation
   commands, local conventions); anything that looks universal is proposed into the template
   instead.
3. Point `CLAUDE.md` at both files.
4. Re-point inbound links from the old AGENTS.md anchors to the satellites (vc-x1's adoption
   commit is the worked example).

## Open questions

For other agents / repos to answer from their own experience:

- **Directory name**: `agent-data/` (adopted in vc-x1) vs `agents/` vs something else.
  `agents/` collides with the harness's `.claude/agents` concept.
- **custom.md shape**: fixed schema of named override points (greppable across repos) vs
  freeform sections (adopted for v1). Does a schema earn its rigidity once several repos have
  one?
- **cycle-protocol.md's home**: stay in `notes/` with cycle.md deferring to it (v1), or merge
  into the satellite tree so cycle content has one file. Merging moves many inbound links and
  the recovery procedures.
- **Always-loaded budget**: is main + custom.md (~220 lines) small enough, and does anything
  in the satellites get missed badly enough that it must move up into the always-loaded core?
- **Pin verification**: is `diff` against the template enough, or is a `vc-x1 validate-agents`
  subcommand worth building once more than one repo adopts?

## The snapshot directory (added 2026-07-31)

[AGENTS-vc-x1-f5-20260730-snapshot/](AGENTS-vc-x1-f5-20260730-snapshot/) holds the complete
universal file-set as a copyable tree: `AGENTS.md`, `CLAUDE.md`, and `agent-data/`, all
verbatim (no annotation headers, so an adopter's copy stays byte-identical to the snapshot and
a pin-style `diff` works). This rehearses the promotion mechanism: at promotion the template
grows the same tree at top level as the real pin target. Adoption mechanics and the adopter
registry live in [snapshots.md](snapshots.md); this section keeps the artifact facts.

- capture taken 2026-07-31 from vc-x1's live copy, the dogfood window's authority; it includes
  the satellite amendments dated 2026-07-30 in vc-x1's custom.md dogfood log (the main file is
  unchanged since the freeze, verified byte-identical to
  [AGENTS-vc-x1-f5-20260730.md](AGENTS-vc-x1-f5-20260730.md) minus that file's header comment)
- the snapshot is frozen: later vc-x1 amendments do not chase into it; an adopter diffs its
  base against vc-x1's live copy to see exactly what moved since adoption
- it is an adoption artifact, not the future pinned `agent-data/`; when promotion creates the
  real top-level tree, this directory stays as history
- links from `agent-data/` upward to `../custom.md` and `../notes/` dangle inside the template
  by design: those files are per-repo and not part of the universal set
