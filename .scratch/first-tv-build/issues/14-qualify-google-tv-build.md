# 14 — Qualify the complete viewing loop on Google TV

**What to build:** Produce the first installable test build with reproducible checks and evidence that the agreed setup-to-watch-to-return flow works on the user's Google TV.

**Blocked by:** 06 — Recover failed channel starts without trapping navigation; 10 — Hide and restore groups and channels; 11 — Reorder groups and channels with the remote; 12 — Expose supported playback and track controls; 13 — Add optional program information without blocking channel access

**Status:** ready-for-agent

**Type:** task

- [ ] A reproducible internal APK and installation/test instructions are available, with the actual dependency/toolchain configuration recorded.
- [ ] The agreed flow is exercised end to end: direct provider setup, personal Home/Guide, search/groups, playback, overlay, mini player, and return to browsing.
- [ ] App/process restart, TV restart, and catalog-refresh checks retain favorites, recents, visibility, order, and meaningful browsing context; combined hide/reorder behavior is covered.
- [ ] Remote navigation during playback and recovery is exercised without lost focus, unintended retuning, trapped Back navigation, crashes, or an unbounded retry spinner.
- [ ] The tested TV model/OS and representative stream capabilities are recorded with sanitized evidence, including observed startup, tuning, frame behavior, and memory; missing physical tests remain explicitly unverified.
- [ ] Build/test success is distinguished from public-store readiness and broad device/provider compatibility; first-build completion is claimed only for checks actually demonstrated.
- [ ] Documentation states which later public-release work remains, including phone setup, billing/trial, schedule grid, and release qualification.
