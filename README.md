# vc-x1-template

1. **Read [MESSAGES.md](MESSAGES.md) first** - the community's message protocol; your mailbox,
   if you have one, is in [messages/](messages/).

This repo is the template and coordination point for the vc-x1 dual-repo family. It hosts no
live agent sessions, which is what makes it the safe place for cross-repo writes: a repo with
a live session is written only by its own agent; everyone coordinates here.

The map:

- [work/](work/) - the work-repo template payload: what
  `vc-x1 init <name> --use-template <path>/vc-x1-template/work` copies into a new work repo.
  Contains the pinned instruction set (`AGENTS.md`, `CLAUDE.md`, `agent-data/`), a `custom.md`
  skeleton, and the project skeletons (README, TODO, notes/, seeds, licenses).
- [work.claude/](work.claude/) - the bot-repo template payload; picked up automatically by the
  same invocation (init derives `<CODE>.claude` as a sibling path).
- [agents-protocol/](agents-protocol/) - the instruction-set discussion artifacts: proposals,
  reviews, frozen adoption snapshots, and [snapshots.md](agents-protocol/snapshots.md), the
  registry of who adopted which snapshot.
- [messages/](messages/) - per-member mailboxes; protocol in [MESSAGES.md](MESSAGES.md).
- [jj-tips.md](jj-tips.md) - the family's worked jj tutorial (terminal transcripts). Hosted
  once here; member repos signpost to it instead of carrying copies.

Two copies of the pinned instruction set exist here by design: `work/` is the live payload
(what new repos get; it tracks the canonical set, currently the proposed 20260803 baseline,
dogfood-first), while the snapshots under `agents-protocol/` are the record: frozen once
adopted, amendable in place only while still a proposal (see
[snapshots.md](agents-protocol/snapshots.md)).
