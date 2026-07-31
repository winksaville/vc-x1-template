# vc-x1-work-repo-template

<one paragraph: what this project is / status>

## Rust projects: seed Cargo.toml from CargoRust.toml

A Rust project scaffolded from this template should base its
`Cargo.toml` on [CargoRust.toml](CargoRust.toml). Adapt the
`[package]` fields freely; in particular keep the
`[lints.clippy]` section so `unwrap`/`expect` uses are visible
from the first commit — each site then needs an explicit
`#[allow]` + `// OK: …` justification (see AGENTS.md >
Code Conventions). The seed is not named `Cargo.toml` so this
template repo itself isn't mistaken for a cargo project.
(Drop this section when rewriting the README for the scaffolded
project.)

## jj Tips for Git Users

Coming from git, start with these; one home per fact, so this section points rather than
repeats:

- [agent-data/jj.md](agent-data/jj.md): the project's quick reference (command basics, the
  working-copy `@` model, revset addressing) plus the dual-repo linking rules. Pinned and
  human-readable; `agent-data/` holds the universal rule files, not agent-only material.
- The [jj docs](https://docs.jj-vcs.dev/latest/) and
  [Steve Klabnik's Jujutsu tutorial](https://steveklabnik.github.io/jujutsu-tutorial/): the
  maintained tutorials; generic jj pedagogy lives upstream, not in this repo.
- `jj-tips.md` in the template repository (path recorded in custom.md): the family's worked
  tutorial with terminal transcripts, e.g. why `jj log` shows fewer commits than `gitk --all`
  and how force-pushes look in jj.

## License

Licensed under either of

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or http://apache.org/licenses/LICENSE-2.0)
- MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the Apache-2.0 license, shall
be dual licensed as above, without any additional terms or conditions.
