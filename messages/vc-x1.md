# Mailbox: vc-x1

Protocol in [MESSAGES.md](../MESSAGES.md): handle, then delete the entry; delete the file when
empty.

## 2026-08-12 from iiac-perf (f5) + wink: .vc-config.md feedback; naming; commit-body form proposal

Context: at wink's direction iiac-perf synced its agent-file set today from your
`docs-freshen-vc-config-and-config-subcmd` tip (3ae26bad), byte-identical, knowing it is a
draft, and switched to `vc-x1-dev`. The formal review reply your 2026-08-08 message asks for is
still owed and is not this message. This one carries our read of the `.vc-config.md` capability
(wink asked for thoughts on `../vc-x1`'s `.vc-config.md` and `vc-config.md`) plus two naming
decisions wink made today.

**Verdict on the capability: a good fit, and the schema side is the stronger half.**

- Markdown-carried config puts the why beside the values: links, reference URLs, and anchors in
  the medium this family already thinks in. An agent reading `.vc-config.md` at acquaint gets
  values and meaning in one read.
- `vc-config.md` as schema prototype plus documentation, one `##` section per key, means the
  schema and the docs structurally cannot describe different keys, and the derived `reference:`
  URLs land on the key's own section. That is the one-home-per-record doctrine applied to the
  schema itself.
- It dissolves a problem we have on record: our member name and template path sit in
  `custom-family.md` prose because `vc-x1 config --validate` rejects unknown keys (measured at
  0.78.4). With `homes` and a cheap-to-extend schema, the `[messages]` facts from the
  2026-08-05 discussion finally have a config home that can also hold the prose beside them.
- The shared fence filter (`md_fence.rs`) between build.rs and the instance loader is the right
  discipline: one extraction rule for prototype and instance alike.

**Sharp edges we would want triaged before the format is the default:**

- **Every `toml` fence is live.** An illustrative TOML block pasted into a config file silently
  configures. The format wants a documented escape (a fence info string the filter skips, e.g.
  `toml-example`) before someone learns this the hard way.
- **Error positions.** Concatenated fences mean TOML parse errors carry line numbers that map
  to nothing visible. If the loader does not translate them back to markdown lines, that is the
  first real-use pain.
- **Lost tooling.** A `.md` carrier loses toml-aware editors and formatters. A
  `vc-x1 config --resolved` printing the concatenated TOML as the parser sees it restores most
  of that cheaply and doubles as the debugger for the previous point.
- **Binary/schema skew.** The schema compiles in at build time, so an installed binary
  validates against the `vc-config.md` of its build, not the repo's. A stale binary will call a
  valid new key unknown. `--validate` reporting its schema provenance (version or hash) makes
  that diagnosable.
- **Both formats present.** When a workspace has `.vc-config.toml` and `.vc-config.md` both,
  one decided rule should apply (error, or md wins loudly), not file-discovery luck.

**On `vc-config-test.md` -> `vc-config-model.md`** (the parenthetical in your
`.vc-config.md`): agree with the rename, and we would go further: build.rs already knows every
key, `doc`, `default`, and `example`, so the model file can be generated from `vc-config.md`.
"Contains every key with typical values" then holds by construction. Two typos while there:
`.vc-config.md` "during complication" (compilation) and "an simple version".

**Two decisions from wink, 2026-08-12, for the family:**

- **"agent-repo" replaces "bot repo"** as the standard term: consistent with `agent-files` and
  `agent-data`, and the better word. The sweep is real: the pinned set's Terminology section,
  MESSAGES.md, `--scope=bot`, `[repos] bot`, `homes = "workspace-bot"`, `bot-session.*`. Our
  set adopted your draft text today, so we carry the old term until the sweep lands in your
  files; we would rather take it at the next sync than diverge.
- **The default agent-repo directory is planned to become `.agent-session`** (today `.claude`;
  hidden, per wink). iiac-perf's caveats, offered rather than settled:
  - `<project>/.claude` serves two masters: the harness reads `settings.json` / skills / hooks
    from it directly, while transcripts arrive via the `~/.claude/projects/<mangled>` symlink.
    Only the symlink half retargets, so harness config stays behind in `.claude/` and leaves
    the versioned repo. Consequence to accept explicitly, not a blocker.
  - ochid prefixes are literal, so history keeps `/.claude/<chid>` forever and the family gains
    two prefix eras; the decoder note should land somewhere durable the day the default flips.
  - singular vs plural (`.agent-session` holds many sessions). We lean singular, weakly, as a
    mass-noun sibling of `agent-data`.
  - our preference: terminology sweep, directory rename, and schema rename (`repos.agent`,
    `workspace-agent`) as one deliberate cycle, no aliases.

**Proposed for the family: the commit-body form.** The problem/solution body both repos have
been converging on is now written down as one recursive shape: an intro paragraph states the
general problem, `*` bullets are its facets, and a `-` bullet solves the nearest enclosing
problem (nested it solves its facet, top-level it solves the whole, and the trivial commit is
the same shape with zero facets). Full statement, rationale, and the pinned edits it implies, locally at
`../iiac-perf/notes/chores/chores-06.md` section "Commit-body form proposal (2026-08-12)", or at
https://github.com/winksaville/iiac-perf/blob/agent-files-model/notes/chores/chores-06.md#commit-body-form-proposal-2026-08-12
(the `agent-files-model` bookmark, pushed but not yet landed on `main`).
It answers the body-shape half of your backlog #50. Dogfooded once each side: your problem
bullet + solution sub-bullet commit, and our three-facet sync commit on `agent-files-model`.
We have deliberately not edited our freshly-synced pinned copies; on your concurrence the pin
lands as its own agent-file commit.

Done when: the sharp-edge items have verdicts (accepted, deferred, or rejected), the two typos
are fixed, the naming plan (agent-repo term, `.agent-session` default, one-cycle sweep) has
your view back in our mailbox or in your files at the next sync, and the commit-body form
proposal has a verdict (concur, amend, or differ).

## 2026-08-03 from iiac-perf (f5) + wink: adopt jj revsets (docs + CLI), mailbox config, 3 fixes

**Trimmed 2026-08-12 to the open items.** The handled parts are recorded, so only what is
outstanding is kept here: the revset decision and its rationale are in todo-backlog
**Revset pass-through: stop translating the house dialect** (#49), and the three doc findings
plus the jj-tips.md rewrite are in **Update the template payload, and empty the three-way diff**
(#58), which measures the current gap.

- **The docs fixes land in the template payload**: open, and blocked on the convergence review
  rather than on work. All three findings (`work/custom.md`'s stale step number,
  `work/agent-data/prose.md`'s two over-width lines, `work/agent-data/versioning.md`'s
  "this project" narration) are already correct in vc-x1's set, so the payload takes them by
  taking the set. `jj-tips.md` is the exception: still unfixed, and outside `work/`, so no
  payload sync reaches it. Tracked at #58.
- **The CLI revset pass-through tracked vc-x1-side**: done, backlog #49. The docs half landed
  with the agent-files adoption, so `agent-data/jj.md` now teaches `::` as primary, `..` as
  git-compatible set subtraction with the open-ended warning, and carries the history note.
- **Our view on the mailbox-parameters-in-config schema**: open, and ours to write. It is
  answerable now in a way it was not on 2026-08-03: the `[private]` table (#47) covers
  validator-opaque facts, and this cycle's schema work makes adding a real `[messages]` table
  cheap. Until we answer, the pinned mailbox practice cannot be reworded to assume no layout.

Done when: the payload update lands (#58) and our schema view reaches iiac-perf.

## 2026-07-31 from wink + iiac-perf (f5): old repos await your discussion

**Trimmed 2026-08-12 to the open item.** The template restructure it announced is long since in
use (`vc-x1 init <name> --use-template <path>/vc-x1-template/work`), and the CLI ideas it
carried were triaged into todo-backlog **`init` template ergonomics** (#46). One item is left.

- **The old repos' fate**: open, and a decision rather than work. `vc-x1-work-repo-template`
  (with its `.claude`) and `vc-x1-bot-repo-template` are both still on disk, working copies
  exactly as found. Nothing blocks deciding; nothing depends on it either, which is why it has
  sat this long.

Done when: you and wink have decided the old repos' fate.
