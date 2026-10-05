# 12 — Expose supported playback and track controls

**What to build:** Use the active stream's supported pause, seek, audio, and subtitle controls consistently in full-screen and mini-player viewing.

**Blocked by:** 09 — Keep playback in a mini player and restore browsing context

**Status:** ready-for-agent

**Type:** task

- [ ] Transport and seek controls reflect the current player/stream capabilities instead of promising rewind or a retained pause position on every channel.
- [ ] An expired paused position presents an understandable route back to live playback rather than an unexplained spinner or silent invalid seek.
- [ ] Available audio and subtitle tracks can be selected, with useful handling when tracks are absent or change on the next channel.
- [ ] Controls → Audio/Subtitles exposes available tracks; selection confirms the change, and Back dismisses the top track menu and restores its trigger without cancelling the underlying session/recovery.
- [ ] Mini-player expansion preserves pause and current position; selecting a channel/Favorite/Recent requests live playback. Warm return offers Resume only when the retained position is valid, otherwise Watch live/Return to live.
- [ ] Remote media buttons and visible controls act on the same playback owner in full-screen and mini-player states.
- [ ] No recording, provider catch-up, or dedicated app-managed time-shift buffer is introduced.
- [ ] Capability-driven tests cover seekable/non-seekable live streams, pause expiry, track changes, and background/foreground control behavior.
