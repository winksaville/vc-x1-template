# MESSAGES.md - the community's message protocol

How members of the vc-x1 dual-repo family leave word for each other. A member is a human or a
repo's agent; a repo with a live session is written only by its own agent, so messages to it
land here instead.

Members: wink, vc-x1, iiac-perf, zc-ring-x1.

The protocol:

- **Mailboxes** are per-member files: `messages/<member>.md` (e.g. `messages/vc-x1.md`).
- **Created on demand, deleted when empty**: a mailbox exists only while something is pending,
  so `ls messages/` shows the community's open traffic at a glance and an absent file is a
  free no-op.
- **Each message** is a dated `##` entry with the sender in the header and a "Done when" line,
  so the recipient knows what closes it.
- **The recipient deletes** a message once handled (jj history is the archive; mailboxes hold
  only open items).
- **Messages are thin pointers, not state**: durable coordination state lives in topical files
  (e.g. the registry in [agents-protocol/snapshots.md](agents-protocol/snapshots.md)); a
  message says "action needed, see <file>" rather than restating the details.
- **Polling**: each repo's `custom.md` carries an acquaint-time line to check its mailbox
  here. Humans check by habit; agents need it written into their instructions.
