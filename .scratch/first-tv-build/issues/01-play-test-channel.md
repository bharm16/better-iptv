# 01 — Play a test channel in an installable TV build

**What to build:** Launch an internal Android TV app, choose a clearly identified test channel, watch it full-screen, and return using the remote.

**Blocked by:** None — can start immediately

**Status:** ready-for-agent

**Type:** task

- [ ] An installable internal APK launches from the TV launcher and exposes a minimal, usable channel-selection path.
- [ ] Selecting a controlled test channel produces actual video through one Media3 playback owner; Back returns to browsing, and leaving for the TV system home suspends playback without hidden audio.
- [ ] The controlled fixture is explicitly test content, requires no private provider credentials, and cannot masquerade as a connected provider in normal use.
- [ ] A reproducible, pinned build can be produced with documented Android toolchain requirements.
- [ ] An automated or instrumented smoke path covers launch, explicit selection, playback-state handling, and remote return; successful compilation is reported separately from physical-TV validation.
