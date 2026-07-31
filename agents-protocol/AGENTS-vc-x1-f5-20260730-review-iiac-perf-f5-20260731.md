# Review: AGENTS-vc-x1-f5-20260730, from the iiac-perf side

A review of the frozen proposal snapshot
[AGENTS-vc-x1-f5-20260730.md](AGENTS-vc-x1-f5-20260730.md) and its companion
[notes](AGENTS-vc-x1-f5-20260730-notes.md), written from the perspective of an agent operating
in iiac-perf under that repo's current pre-restructure AGENTS.md (one ~600-line always-loaded
file). Sources read: the two snapshot files; vc-x1's live AGENTS.md, custom.md, and
agent-data/cycle.md; iiac-perf's AGENTS.md and TODO.md. The scope-name and push-stamping
claims below were checked against vc-x1's source at HEAD and the locally installed vc-x1
binary, not taken from the docs.

Authored 2026-07-31 by Claude (Fable 5) in an iiac-perf session, with Wink. Sibling of
[iiac-perf-comments.md](iiac-perf-comments.md) (2026-07-30), which commented on the
pre-restructure unification effort; this file reviews the restructure proposal itself.

## Verdict

The proposal is sound, and its diagnosis matches this reviewer's experience operating under
the old files. The rules that get broken are procedural invariants that must fire at a
specific moment; spread across ~1,800 always-relevant lines of narrative, they are recalled
from a compressed memory at exactly the moment precision matters. Both design moves target
that failure directly:

- a short always-loaded core of numbered hard rules
- satellites with checklists above rationale, read at the moment of action

The 12 hard rules are the right 12: they are the historically violated ones (pre-committing a
rung, the post-push hard stop, hand-written ochids, title identity, punctuation).

## From the acting agent's perspective

- **The always-loaded core is what actually conditions behavior.** Satellites read "at the
  moment of action" only help if the agent remembers to read them, which is itself the recall
  problem being fixed. The design handles this correctly by promoting the costliest
  invariants into the core (a skipped satellite read then degrades style, not safety), and
  hard rule 7 forces the one read that matters most.
  - We think the mechanism behind skipped reads is the same incentive gap
    iiac-perf-comments.md measured for command bundling: the read costs a visible tool call
    every time, while skipping it costs nothing until something breaks.
  - If dogfooding shows satellite reads getting skipped, a harness hook (a reminder keyed on
    the action, not on memory) is the mechanical fix; worth holding in reserve, not building
    now.
- **Checklists-first is right.** Mid-task an agent reads the top of a file and stops when it
  has what it needs; cycle.md as built honors this.
- **Numbered hard rules make violations nameable**, which feeds the dogfood log with citable
  evidence. A good loop.
- **custom.md wins-conflicts works only while custom.md stays small.** vc-x1's is currently
  in good shape (medium/validation, two overrides, dogfood log). A fat custom.md would
  recreate the original problem with precedence rules stacked on top.

## Findings from the iiac-perf comparison

Concrete items surfaced by diffing the proposal against iiac-perf's AGENTS.md; each is either
dogfood evidence or a migration precondition.

- **Scope-name drift, a real pinning hazard.** iiac-perf's AGENTS.md says the work-repo scope
  is `code`; the proposal says `work`. The vc-x1 binary installed on this machine still
  accepts `code|bot`, while vc-x1's source at HEAD has renamed it to `work`. A pinned
  universal file therefore bakes in a CLI-surface fact that varies with the installed binary.
  - proposal: the template should state a minimum vc-x1 version, and the migration sketch
    should couple "take a template update" with "upgrade vc-x1" as one step.
- **A semantic conflict to resolve at migration.** iiac-perf's AGENTS.md permits `jj commit`
  plus a hand-written `ochid:` for a commit "pushed later as a non-top commit", on the ground
  that push stamps only the topmost commit. Hard rule 5 says never hand-write ochids, and
  cycle.md says push stamps each new commit's trailer.
  - if vc-x1 now stamps every commit it creates, iiac-perf's exception is obsolete and drops
    at migration; if not, the hard rule forbids a workflow iiac-perf documents
  - needs a check against actual push behavior, not the docs on either side.
- **Live evidence for the maintenance half of the problem statement.** Hard rule 8 (typeable
  punctuation) is a template hard rule, yet in iiac-perf the same rule sits unlanded on the
  parked `punctuation-sweep` bookmark (its Todo #2), and TODO.md's links to
  `AGENTS.md#typeable-punctuation-only` dangle on main. That is the propagation failure the
  companion notes describe, observed in the wild.
  - practical corollary: iiac-perf should land that branch before migrating, or the sweep and
    the migration collide in AGENTS.md.
- **Conventions that changed under the older repos' feet.** The dogfood log already amended
  title width (iiac-perf: <=50; template now <=72) and docs wrap (<=72 vs <=100). Fine
  changes, but migration sketch step 2 should distinguish "local delta that moves to
  custom.md" from "local habit the template now overrides"; iiac-perf has both kinds.

## Answers to the open questions

- **Directory name**: `agent-data/` is fine; the `agents/` collision with the harness concept
  is real, do not fight it.
- **custom.md shape**: keep freeform, but vc-x1's file already shows a de-facto three-section
  shape (Medium and validation / Project conventions and overrides / Dogfood log). Codify
  those three `##` headers as a soft convention: greppable across repos without a schema's
  rigidity.
- **cycle-protocol.md's home**: stay in `notes/` for v1; cycle.md's "on disagreement, the
  protocol wins" line is sufficient glue.
- **Always-loaded budget**: ~220 lines is right. Nothing in the satellites needs promotion:
  the two mid-checklist stops (per-commit steps 5 and 7) are the costliest satellite content,
  and hard rule 2 already covers their substance.
- **Pin verification**: `diff` suffices during the dogfood window; `validate-agents` earns
  its keep at promotion, especially since it can also check the CLAUDE.md wiring and a
  minimum-CLI-version stamp.

## Adoption stance for iiac-perf

Yes in principle; at promotion, not mid-window. Adopting now would fork a draft that vc-x1 is
amending freely, recreating the drift problem the proposal exists to fix. The designed flow
(authority returns to the template at promotion, then other repos migrate) is the right
moment. Preconditions for iiac-perf, from the findings above:

- land the parked `punctuation-sweep` branch first
- upgrade the installed vc-x1 past the `code` -> `work` scope rename
- resolve the non-top-commit ochid question against actual push behavior

## A convention for review files

This file's name proposes the convention: a review of a discussion snapshot is named

```
<target-basename>-review-<reviewer-repo>-<reviewer-model>-<date>.md
```

so this file, a 2026-07-31 review by Fable 5 from iiac-perf of `AGENTS-vc-x1-f5-20260730.md`,
is `AGENTS-vc-x1-f5-20260730-review-iiac-perf-f5-20260731.md`.

- the target's basename prefix keeps a proposal, its `-notes`, and its reviews adjacent in a
  directory listing
- reviewer repo + model + date in the suffix mirror the snapshot convention's author
  identity, allow multiple reviewers per proposal, and allow re-reviews on later dates
- the names run long, but these are discussion artifacts: written once, read by browsing,
  never typed in anger

The earlier free-form `iiac-perf-comments.md` predates the convention and keeps its name.

## Addendum 2026-07-31: rule 0 and hard-rules-first

An amendment applied to the snapshot's `AGENTS.md` the same day, authored snapshot-side
because vc-x1's session was live (see the pending-sync note in [snapshots.md](snapshots.md)).
The gap, spotted by Wink: AGENTS.md mentioned custom.md five times, every one descriptive
("is always loaded", "wins conflicts"), never a single explicit imperative to read it. The
intro's "always loaded" claim is also only true under Claude Code's CLAUDE.md import wiring;
an AGENTS.md-aware tool like Zed loads the root AGENTS.md alone and follows no `@` imports,
so under any other harness custom.md was invisible and nothing ordered the read.

The amendment, three connected changes:

- **Rule 0 added**: "Read custom.md before acting on anything below", carrying the precedence
  fact, with "already satisfied if your harness auto-loaded it" so it is a no-op where the
  wiring works. Numbered 0, not a new 1: it is a precondition rather than a peer prohibition,
  and rules 1-12 keep their numbers, so existing by-number citations stay valid (GitHub
  renders an ordered list starting at 0 correctly).
- **Hard rules moved first**, directly under the title: the file preached checklists-first
  but opened with meta and the dual-repo model before its own rules. The cost, rules using
  terms defined below them, is accepted: the file is optimized for re-reading by an agent
  mid-task, not first contact, and each rule links to its detail.
- **The "How to read this set" bullet list dissolved**: its custom.md content became rule 0,
  its satellites content already lived in the file map (whose heading now also carries
  "immediately before acting, not from memory" and "checklists first, rationale after" so the
  phrases survive). The false harness-specific claim is the one thing deleted outright.
