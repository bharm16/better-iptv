---
status: accepted
---

# Native Android foundation for the first two TV targets

Use Kotlin, Compose for TV, and Media3/ExoPlayer for Google/Android TV first and Android-based Fire OS next. The user accepted this direction subject to research, and the [stack comparison](../../.scratch/product-discovery/research-stack.md) supports it for the selected platforms; React Native TV remains a credible alternative if near-term Apple TV delivery changes the priorities. Keep provider/catalog/personalization rules separate from Android UI, storage, and playback integration so that later ports can retain those rules.

## Consequences

- Use Compose for the interface with a dedicated Media3 video surface. Allow a narrow View integration if a demonstrated capability gap requires it.
- Start with one Media3 playback integration; add another engine only for a reproduced compatibility benefit that justifies its additional behavior and qualification work.
- Pin and qualify the actual dependency combination, device/OS range, and required stream formats before claiming support. Documentation research does not establish measured reliability or performance.
- Apple TV and Vega still require separate interface/playback work. This decision does not select a Kotlin Multiplatform build, a QR-setup transport/backend, or a cloud service.
