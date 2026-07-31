# vc-x1-bot-repo-template

This is the bot repo of a dual-repo convention for using
a bot to help in the development of a coding project. The goal
is that this bot repo contains the "why" and "how", while the
partner main repo contains the "what". The key to the convention
is each change is cross-referenced to the other. Thus there
is a coherent story of the development of the project across time.

## Reading a commit here

Each commit here records the transcript written since the
previous commit, usually a slice of a conversation still in
progress, and is paired with a commit in the work repo,
cross-referenced by an `ochid:` trailer in both directions.
Its diff is one or more transcript files, but its body is the
**work** commit's body: a file-by-file list of what changed
over there.

- That is deliberate. The pair's story reads whole from either
  side, so `git log` here says what the work was without
  switching repos.
- It does mean the bullets name files this repo does not
  contain. Follow the `ochid:` trailer to reach the diff they
  describe.

## Template contents

This repo is the source template for the bot side:
[vc-x1](https://github.com/winksaville/vc-x1) `init` copies its
contents (the licenses, this README.md, and the
`memory/MEMORY.md` stub) into a new project's `.claude` repo,
then generates the remaining minimum files (such as
`.vc-config.toml`) itself. The stub points at the committed
instruction files and is expected to stay a stub; it is seeded
here because Claude tends to create it otherwise.

This payload's work-repo counterpart is `work/`, one directory up in the template repository;
the family map is in the template's root README.md.

## License

Licensed under either of

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or http://apache.org/licenses/LICENSE-2.0)
- MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the Apache-2.0 license, shall
be dual licensed as above, without any additional terms or conditions.
