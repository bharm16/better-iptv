# 04 — Return to recently watched channels

**What to build:** Find channels that actually played in a persistent Recents list on Home and the Guide and return to their current live broadcast.

**Blocked by:** 02 — Connect a provider and watch its channels without guide data

**Status:** ready-for-agent

**Type:** task

- [ ] A recent entry is added only after successful channel playback; highlighting a channel, loading it unsuccessfully, or opening its details does not count as watching.
- [ ] Entries are deduplicated by provider/channel identity and sorted by most recent successful viewing.
- [ ] Home and the Guide use the same recent history, retained across app/process restarts.
- [ ] Selecting a recent entry tunes the channel live; it does not imply resuming an earlier program or a saved recording.
- [ ] Missing channels are handled explicitly without guessing a replacement or deleting unrelated history.
- [ ] Tests cover successful and failed starts, repeated visits, ordering, persistence, and returning to live.
