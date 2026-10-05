# Stack decision research for Better IPTV

Researched: 2026-10-04. This is primary-source documentation research against the agreed product scope. No application, dependency combination, provider stream, physical device, or comparative benchmark was executed.

## Recommendation

**Use Kotlin, Compose for TV, and Media3/ExoPlayer for the initial app.** This is the best-supported fit for the selected Google/Android TV first, Android-based Fire OS second roadmap. It is an engineering judgment about fit and integration boundaries, not proof that native code is inherently faster or less buggy than another framework.

The strongest alternative is React Native TV. Flutter is viable on Android but carries more unresolved TV-platform work in the first-party evidence reviewed. Keep application rules separate from UI and playback so that a later platform change does not require redefining the product.

## Why the selected platforms matter

The first two targets share Android foundations. Amazon documents an Android-app path for Fire OS, with differences in services, hardware, controls, and store integration that still require attention. The shared foundation favors a native Android implementation now; it does not qualify every Fire TV model. Vega OS is a different target and is outside the selected next port. [Amazon Android/Fire OS development comparison](https://developer.amazon.com/docs/fire-tv/differences-from-android-tv-development.html), [device/OS matrix](https://developer.amazon.com/docs/fire-tv/fire-os-overview.html).

The initial product needs remote navigation, local personalization, one active live player, browsing over playback, and graceful handling of absent guide data. It does not yet need shared mobile/web screens, tvOS delivery, recording, a custom live buffer, or cloud profile synchronization. Those scope choices reduce the immediate value of a second UI runtime. This is a project-specific assessment, not a limitation of cross-platform frameworks.

## UI alternatives

| Candidate | Primary evidence | Assessment for this app |
| --- | --- | --- |
| **Kotlin + Compose for TV** | Google provides TV components and focus-oriented Foundation lists; current TV Material has a stable release. [TV toolkit](https://developer.android.com/training/tv/playback/compose), [TV list guidance](https://developer.android.com/training/tv/playback/compose/lists), [releases](https://developer.android.com/jetpack/androidx/releases/tv). | Preferred for the two selected Android targets. Use Compose for the interface without insisting that every integration must be implemented entirely in Compose. |
| **React Native TV** | The community TV fork implements native focus events, focus guides, and TV-aware virtualization. Expo documents compatible TV libraries and SDK/fork alignment. [TV fork](https://github.com/react-native-tvos/react-native-tvos), [Expo TV guide](https://docs.expo.dev/guides/building-for-tv/). | Credible runner-up, especially if Apple TV becomes a near-term commitment or existing React expertise dominates the delivery plan. It is not a WebView and has not been shown slower here. |
| **Flutter** | Android apps can run on Android TV, but Flutter's Android-team tracker identifies remaining TV input, focus, tooling, and testing gaps. [TV support tracker](https://github.com/flutter/flutter/issues/180542). | Not the preferred starting point for this TV-only project without an already-qualified Flutter TV/player foundation. The evidence does not mean Flutter cannot deliver a good app. |

React Native's media layer requires an explicit version decision. React Native Video v7's introduction advertises tvOS while the repository feature table still marks TV support TODO; v6 is maintained, and Expo Video is another candidate. Treat the conflicting v7 claims as a qualification issue, not proof that it cannot work. [V7 introduction](https://docs.thewidlarzgroup.com/react-native-video/docs/v7/fundamentals/intro/), [project status](https://github.com/TheWidlarzGroup/react-native-video), [Expo Video](https://docs.expo.dev/versions/latest/sdk/video/).

Legacy Leanback is deprecated, so it is not a stronger default for a new app. A narrowly scoped Android View integration remains reasonable if it fixes a demonstrated limitation. [Leanback status](https://developer.android.com/jetpack/androidx/releases/leanback).

## Refinements to the native recommendation

### Persistence is part of the stack

The original three-library recommendation was incomplete for the user's central complaint. Recommend **Room/SQLite for catalog and personalization data**, with **DataStore for small preferences**. Android's guidance distinguishes larger relational/partially updated data from the small datasets suited to DataStore. These supporting choices are recommendations to carry into implementation planning. [Room](https://developer.android.com/training/data-storage/room), [DataStore](https://developer.android.com/topic/libraries/architecture/datastore).

The app must retain provider/channel identity, favorites, hidden items, ordering, and recents independently of refreshing provider catalogs. This is our design responsibility. Replacing the provider's latest list must not replace the viewer's personal choices.

### Remembered focus is not durable personal data

Compose's focus restoration covers runtime navigation between containers. Separately persist enough identity to reconstruct the desired context after a restart; an old row index is insufficient after lineup changes. [Focus restoration](https://developer.android.com/develop/ui/compose/touch-input/focus/focus-restoration).

Saved UI state and a ViewModel are not substitutes for durable storage. Android distinguishes state that survives recreation from data that survives completing/dismissing the activity. Store small navigation keys in saved state and long-lived personalization on disk. [Android state lifetimes](https://developer.android.com/topic/libraries/architecture/saving-states), [Compose state saving](https://developer.android.com/develop/ui/compose/state-saving).

### Use a dedicated video surface

Start with Media3's dedicated Compose surface integration and a SurfaceView where appropriate. Android documents risks in blindly embedding PlayerView inside AndroidView, while dedicated surface composables handle surface lifecycle. [Surface guidance](https://developer.android.com/media/media3/ui/surface).

Current Media3 has Compose controls with TV D-pad support, but its Compose modules have not reached complete View-module parity. Select the surface/control combination against our actual overlay, subtitle, and track-selection requirements. Preserve a narrow fallback boundary for a demonstrated missing capability. [TV controls](https://developer.android.com/media/media3/ui/androidtv), [module support boundary](https://developer.android.com/media/media3/ui/overview).

### One playback owner, one initial engine

Recommend one playback owner whose lifetime is independent of individual channel cards and overlay composition. Opening the browser must not create another decoder or retune the stream; an explicit channel selection replaces the active media. This is an application design judgment consistent with Media3's resource lifecycle, not a framework feature that happens automatically. [Player lifecycle](https://developer.android.com/media/media3/exoplayer/hello-world).

## Media3 versus LibVLC

Media3 is the preferred first engine. It supports the relevant HLS/progressive-TS paths and provides Android player/session integration. Container support does not establish codec/profile compatibility: platform decoders and output hardware still matter. Other UI frameworks can wrap the same Android engine, so the UI language does not itself improve decoding. [Format matrix](https://developer.android.com/media/media3/exoplayer/supported-formats), [MediaSession integration](https://developer.android.com/media/media3/session/control-playback).

LibVLC is a serious alternative when its input handling or software decoding resolves a required, reproduced gap. First check correct source/extractor configuration; some apparent Media3 failures have documented configuration remedies. An audio-only gap may be addressable through Media3's optional FFmpeg audio decoder rather than another complete player. [VLC Android capabilities](https://images.videolan.org/vlc/download-android.html), [Media3 troubleshooting](https://developer.android.com/media/media3/exoplayer/troubleshooting), [decoder extensions](https://developer.android.com/media/media3/exoplayer/demo-application#enabling-bundled-decoders).

No supplied stream currently demonstrates a reason to ship two engines. A second engine would need its own lifecycle, controls, error interpretation, and qualification coverage. Reconsider it when a controlled comparison demonstrates an important compatibility benefit.

Amazon publishes a Media3 port based on 1.3.1. That is positive Fire OS evidence, but not certification of current upstream releases across all models. Prefer qualifying a current stable upstream release before adopting a vendor fork solely because an older guide mentions it. [Amazon Media3 port](https://github.com/amzn/media3-external-port).

## Maintenance and later portability

The release pages currently list TV Material **1.1.0** and Media3 **1.11.1** as stable. These are research observations, not an already-tested dependency lock. Resolve the full Compose/Kotlin/Android build graph and minimum OS requirement before pinning it; older introductory snippets are not an authoritative compatibility matrix. [TV releases](https://developer.android.com/jetpack/androidx/releases/tv), [Media3 releases](https://developer.android.com/jetpack/androidx/releases/media3).

Keep provider/catalog/personalization rules in platform-independent Kotlin boundaries. Kotlin Multiplatform can share logic with tvOS, but official Compose Multiplatform UI support does not list tvOS. Apple TV and Vega still need distinct UI/player integration. There is no immediate need to add a multiplatform build graph for two Android targets. [Kotlin platform support](https://kotlinlang.org/docs/multiplatform/supported-platforms.html), [Vega porting boundaries](https://developer.amazon.com/docs/vega-api/0.24/porting-libraries).

QR setup does not require the TV UI itself to be cross-platform. Its phone webpage and credential handoff are a separate design concern; choosing Kotlin does not decide whether that transfer is local or relayed. No backend or cloud credential store is selected by this research.

## What must be demonstrated on hardware

These are proposed qualification tasks, not completed checks or authorization to start implementation before the discovery review:

1. **Remote navigation under playback:** navigate a representative large lineup, use held arrow keys, open/close overlays, switch groups/providers, and return from playback without losing meaningful focus or changing channel merely through browsing.
2. **Real required streams:** qualify the delivery formats, codecs, subtitles/audio tracks, and sound output actually encountered. Include rapid channel changes, network interruption, expired live windows, and returning from background.
3. **Continuity:** verify favorites, recents, visibility, and ordering after process termination, app restart, TV restart, and catalog refresh. Test missing or changed channel identities explicitly.
4. **Performance:** measure startup, first video frame, input response, frame jank, dropped video frames, and memory during combined browsing and playback. Use a release build on the user's actual Google TV, then representative Fire OS hardware. An emulator result is not a device benchmark. [Android benchmark guidance](https://developer.android.com/codelabs/android-baseline-profiles-improve).

A measurable native UI bottleneck could justify a focused View hybrid. Required streams that remain broken after correct Media3 configuration could justify LibVLC. A committed near-term Apple TV release or substantial React delivery advantage could justify React Native TV. Those are concrete reasons to revisit the choice; a generic claim of greater cross-platform reach is insufficient for the current roadmap.

## Supporting investigations

- [Native UI risks](./research-native-ui-risks.md)
- [Cross-platform alternatives](./research-cross-platform-options.md)
- [Playback engines](./research-player-options.md)
- [Platform boundaries](./research-tv-platforms.md)
- [Live playback capability distinctions](./research-live-playback.md)
