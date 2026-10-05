# Native Android UI risks and validation boundary

Research date: 2026-10-04. Documentation research only; no device, application, provider, or benchmark was tested. The native stack remains provisional.

**Finding:** Compose-first is defensible for this channel-based app, but requiring every UI element to use Compose is premature. Preserve a narrow View fallback until focus continuity, video presentation, and low-power performance pass a representative spike. Native technology does not itself deliver the viewing contract.

## Components and focus

**Fact:** TV Material 1.1.0 and TV Foundation 1.0.0 are stable. The release history includes a fixed lower-API ExoPlayer rendering defect involving TV Material Surface compositing. This is historical integration evidence, not a claim that the current release remains broken. Pin and test the complete library combination. [TV releases](https://developer.android.com/jetpack/androidx/releases/tv)

**Fact:** Current guidance uses standard Foundation lazy lists/grids; the older TV-specific lazy containers are deprecated. Focus-driven scrolling is built in, with custom positioning through `BringIntoViewSpec`. **Inference:** that covers ordinary channel lists, but a time-based schedule grid still needs explicit geometry and rules for moving vertically between unequal-duration programs. [TV layouts](https://developer.android.com/training/tv/playback/compose/lists)

**Fact:** `focusRestorer` handles runtime container re-entry; process recreation needs separate state restoration. **Inference:** provider/channel identity, remembered location, and fallback after a channel disappears must be app-owned state. A saved list index alone cannot establish continuity after reordering. [Focus restoration](https://developer.android.com/develop/ui/compose/touch-input/focus/focus-restoration)

Focus machinery continues receiving fixes: Compose UI 1.12.0-alpha03 records a fix for repeated save calls breaking restoration. This gives a concrete regression scenario, not comparative defect-rate evidence or proof of a remaining stable-release fault. [Compose UI release notes](https://developer.android.com/jetpack/androidx/releases/compose-ui#1.12.0-alpha03)

## Playback integration

**Fact:** Media3 recommends `SurfaceView` for power/frame-timing advantages; some TVs also need it for full-resolution video. Its documentation warns that `PlayerView` wrapped in `AndroidView` has no compatibility guarantee, identifying Android 14 surface problems. Dedicated `ContentFrame`/`PlayerSurface` provide lifecycle-aware Compose integration. **Inference:** start with a stable surface underneath overlays; do not switch to `TextureView` merely to simplify animation. [Surface guidance](https://developer.android.com/media/media3/ui/surface)

The core Compose module supplies surfaces and player-state holders without styled controls. The Material3 `Player` now supports D-pad navigation, including default focus management; custom slots remain the application's responsibility. Calling Compose playback inherently touch-only would be outdated. [Compose module choices](https://developer.android.com/media/media3/ui/compose), [TV player navigation](https://developer.android.com/media/media3/ui/androidtv)

However, Media3 explicitly says its Compose modules have not reached View-module parity. **Inference:** inventory the actual required controls, subtitles, and track-selection behavior before choosing the UI module. A View-owned playback host is a credible fallback for a demonstrated missing capability; wrapping `PlayerView` blindly is not a universal shortcut. [UI support boundary](https://developer.android.com/media/media3/ui/overview)

## Performance and support

Google's current Compose-versus-Views performance example uses Pokedex journeys; it does not qualify this IPTV UI on the user's TV. Its guidance calls for release mode, R8, and baseline profiles. **Inference:** neither generic benchmarks nor a smooth debug emulator establishes performance during simultaneous video decoding and guide navigation. [Performance guidance](https://developer.android.com/develop/ui/compose/performance)

TV memory guidance gives a 280 MB total target for a 1 GB low-RAM device under its specified single-stream assumptions. Measure graphics/native/media buffers as well as the managed heap. Treat the user's unknown TV and eventual Fire OS model as separate validation targets. [TV memory guidance](https://developer.android.com/training/tv/playback/memory)

Dependency compatibility also needs verification: Foundation's 1.10 release cycle raised its default minimum API from 21 to 23. The stack name does not establish support for every Android-based Fire TV. Validate the resolved dependency graph against the selected OS/device floor. [Foundation releases](https://developer.android.com/jetpack/androidx/releases/compose-foundation#1.10.0-alpha01)

## Required spike before implementation confidence

- Navigate representative large channel lists and unequal-duration schedule rows using a real remote, including held-key repetition, empty groups, missing EPG, refreshed/hidden channels, provider switching, and returning from playback.
- Open/close the channel browser repeatedly during playback. Confirm browsing never retunes or recreates the player; exercise Back, transport keys, focus return, background/resume, subtitles, and direct-TV keyboard entry.
- Measure cold/warm startup, frame jank, remote-response latency, dropped video frames, and peak memory in a release build. Compare an isolated View implementation only where a reproducible failure or measured bottleneck remains.

**Decision rule:** use Compose if those paths pass; select a hybrid only for demonstrated gains. Starting this new app with Leanback would accept a deprecated dependency without evidence of compensating benefit. [Leanback status](https://developer.android.com/jetpack/androidx/releases/leanback)
