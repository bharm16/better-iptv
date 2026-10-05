# 09 — Keep playback in a mini player and restore browsing context

**What to build:** Return from full-screen playback to Home or the Guide with the current channel still playing in a small window and the relevant browsing position restored.

**Blocked by:** 06 — Recover channel starts and interrupted playback; 07 — Switch saved providers without mixing personal channels; 08 — Browse channels over full-screen playback

**Status:** ready-for-agent

**Type:** task

- [ ] Home and the full Guide present the current session in a mini player; selecting it expands the same session without retuning, resuming, seeking or clearing recovery state.
- [ ] Channel selection and mini-player expansion capture the latest browsing destination/provider/collection/query/identity/scroll context. Expanding A while browsing B and then pressing Back restores B, not A's original launch view.
- [ ] Back follows the [interaction contract](../interaction-contract.md): dismiss the topmost keyboard/menu/details/controls/browser layer first; a bare full-screen initial/replacement/retry attempt or its failure is cancelled/cleared. Established playback/recovery minimizes, browsing Back never expands the player, and root Back exits without confirmation or loops.
- [ ] Restoration uses provider/channel identity, then next/previous surviving item, then an enabled group selector, Browse channels or Manage hidden items; a decorative heading is never the fallback.
- [ ] Changing the provider being browsed does not retune the active stream until a new channel is selected; the mini player identifies its active source.
- [ ] A remote-reachable Stop/Close player action exists in full-screen controls and mini-player actions, including pending/error states; it cancels playback/recovery, removes the player and suspended-resume context, and retains browsing and saved personal data.
- [ ] Ongoing buffering/reconnecting, terminal failure and Stream ended stay on the current full-screen/mini surface without taking over the Guide or stealing browsing focus.
- [ ] Backgrounding suspends playback and pending recovery without hidden audio; a player instance need not survive. Warm return restores context with an explicit action and only offers Resume for a valid position; otherwise it offers Watch live/Return to live.
- [ ] Fresh launch and process recreation open Home without autoplay; only successfully viewed channels appear in Recents.
- [ ] Tests exercise full-screen, overlay, Home, Guide, mini-player, provider mismatch, latest-origin restoration, A-to-B cancellation/failure, Stop, post-start interruptions, and warm/cold return while checking session and focus effects.
