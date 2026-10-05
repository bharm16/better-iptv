# 09 — Keep playback in a mini player and restore browsing context

**What to build:** Return from full-screen playback to Home or the Guide with the current channel still playing in a small window and the relevant browsing position restored.

**Blocked by:** 07 — Switch saved providers without mixing personal channels; 08 — Browse channels over full-screen playback

**Status:** ready-for-agent

**Type:** task

- [ ] Home and the full Guide present active playback in a mini player; selecting it returns to full screen without opening a second stream.
- [ ] Back closes overlays first, then returns to the originating browsing view and a meaningful focused item.
- [ ] Restoration uses provider/channel identity rather than only a row index and has a visible fallback when the item no longer exists.
- [ ] Changing the provider being browsed does not retune the active stream until a new channel is selected; the mini player identifies its active source.
- [ ] Fresh app launches remain without autoplay, and leaving the app for system Home pauses video rather than leaving hidden audio playing.
- [ ] Tests exercise full-screen, overlay, Home, Guide, mini-player, and background/return transitions while checking playback continuity and focus.
