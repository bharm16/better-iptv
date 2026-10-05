# First TV wireframe elements

Researched: 2026-10-05. Scope: Google/Android TV, using current primary documentation and official product help/posts. This note recommends a first visual pass; it does not change the accepted [interaction contract](../first-tv-build/interaction-contract.md). No competitor app was run and no screenshot parity is claimed.

**Superseded visual recommendation:** the user rejected the resulting generic card/list layout. The layout and geometry recommendations below were based on text guidance, not inspected TV screens. Use [actual TV guide and Home visual references](research-tv-guide-visuals.md) and the [revised wireframe map](../tv-wireframes/map.md) for the current visual direction. Platform behavior citations remain useful; the original layout is retained as history.

## Recommendation

Build a quiet, text-led Home with **Favorites, then Recent channels**; a channel-list Guide; and one player with full-screen, compact-browser and mini presentations. Use optional channel logos and trustworthy program text as enrichment. Do not build a poster-led Home, a mostly empty schedule grid, or decorative program placeholders. This follows our [channel-first decision](../../docs/adr/0001-channel-access-independent-of-guide-data.md), not a claim that competitors use this exact design.

## What the evidence supports

| Source | Verified guidance or behavior | Application to this first pass |
| --- | --- | --- |
| [Android TV layouts](https://developer.android.com/design/ui/tv/guides/styles/layouts), updated 2025-05-09 | Uses a 16:9, 960×540 MDPI design canvas; gives horizontal/vertical stacks, grids and context-preserving overlays. Key content needs overscan-safe margins. | Use a proportional TV canvas, simple axes and uncluttered regions. Keep controls inside safe bounds; video/background may extend to the edge. |
| [Android TV typography](https://developer.android.com/design/ui/tv/guides/styles/typography), updated 2026-07-06 | Recommends larger, immediately legible text for distance; Roboto is the default. Titles suit cards and lists; display styles are for short, prominent text. | Use Roboto and a small hierarchy. Channel identity gets more emphasis than optional program metadata. Numeric sizes below are our proposal, not platform minimums. |
| [Android TV focus system](https://developer.android.com/design/ui/tv/guides/styles/focus-system) | One element receives focus. Focus can use outline, surface, scale and glow; focused and pressed states are distinct. | Give every interactive component an obvious focus treatment. “Playing” and “Favorite” are persistent status, independent of focus. |
| [Android TV navigation](https://developer.android.com/training/tv/get-started/navigation), updated 2026-09-08 | All visible controls must be D-pad reachable; directions should have predictable roles. Back must reach the launcher without exit gates or loops. | Annotate focus routes and return targets. Preserve the contract’s explicit Back precedence; never use Back as a player-expansion shortcut. |
| [Android TV tabs](https://developer.android.com/design/ui/tv/guides/components/tabs), updated 2026-03-30 | Tabs represent peer destinations. Pill indicators suit full-page destinations; bar indicators suit subdivisions. Focused and selected are separate states. | A restrained top row can hold Home and Guide; provider/group controls belong below it. Selected Home must remain identifiable while a channel has focus. |
| [Android playback controls](https://developer.android.com/training/tv/playback/controls), updated 2025-04-17 | Center plays/pauses; Up/Down reveals information without pausing; Left/Right seeks. | The proposed “OK opens controls” shortcut diverges from the documented default. Prefer the mapping below for the first test; expose only playback capabilities the stream actually supports. |
| [Fubo favorites](https://support.fubo.tv/hc/en-us/articles/360028439511-How-do-I-Favorite-the-channels-I-watch-most), updated 2024-05-08 | Favorites appear at the beginning of Home and Guide; TV channel actions use a menu and confirmation. Device appearance can vary. | Stable familiar channels and visible channel actions have direct precedent. Our channel-body selection still tunes immediately; do not copy Fubo’s menu-first selection literally. |
| [Fubo Browse While Watching](https://support.fubo.tv/hc/en-us/articles/360002868712-How-can-I-browse-other-programming-while-watching-my-current-channel), updated 2025-03-11 | TV Down opens browsing; Left/Right inspects other programs; OK switches; Back closes browsing and retains the current channel. | A bottom channel browser with explicit selection and dismiss-without-switch behavior is supported. Its corner mini-player examples are in the web/mobile sections, not proof of a TV mini layout. |
| [Sling player feature announcement](https://www.sling.com/whatson/announcements/new-features), 2025 rollout | Describes Recent/Favorite Channels near player controls and Up for Browse and Watch. The announcement says most Roku devices first, with other devices rolling out during 2025. | Personal channel browsing during playback is a useful precedent. Do not claim that this exact placement or key mapping is verified on current Android TV. |
| [YouTube TV watching help](https://support.google.com/youtubetv/answer/7067974/watch-shows-sports-events-amp-movies), undated, checked 2026-10-05 | Home, Live and Library serve different tasks; Live can hide/reorder networks. TV startup autoplays a recommendation unless disabled. | Distinct Home/Guide views and explicit organization are defensible. Our quiet startup and channel-first Home are deliberate product choices; do not add Library, DVR or autoplay by analogy. |

The evidence supports components and navigation conventions, not our session ownership, focus restoration, finite recovery budgets or A→B replacement policy. Those come from the project contract. Official help is documentation, not hands-on usability validation.

## First-pass component and layout specification

All geometry below is a **proposal to test on a TV**. Units are design dp unless stated otherwise. A 1920×1080 Figma frame can render the 960×540 layout at 2×; double the drawing dimensions, not the implementation dp/sp values.

| Element | Proposed specification |
| --- | --- |
| Canvas and spacing | 960×540 logical canvas. Use 58 horizontal and 28 vertical safe margins, leaving 844×484. Base spacing 4; ordinary gaps 12–20. Android’s layout page inconsistently gives 48/27, rounded 24, and 58/28 margins. The 58/28 choice is our conservative grid convention, not a single universal platform rule. |
| Type | Roboto: 28/34 screen title, 22/28 shelf heading, 20/26 channel name, 18/24 navigation/action, 16/22 optional metadata and hints. In Figma at 2× these become 56, 44, 40, 36 and 32px. Avoid thin text and paragraph-heavy cards. Verify long channel names at couch distance. |
| Global header | Compact top navigation: Home, Guide and a clearly labeled Settings action. Below it, show the browsed provider and relevant collection/group/search controls. Identify a different playing provider on the mini player when necessary. No large hero region. |
| Focus state | High-contrast 2dp outline plus a clear surface change; reserve outline clearance. A modest 1.025 scale is optional for cards, unnecessary for dense list rows. Use a separate Playing badge and favorite marker. Pressed state must visibly differ. Do not rely only on color, glow or tiny icon changes. |
| Home channel card | Four 196dp-wide cards with 20dp gaps when using the full 844dp width. Start around 112dp high: optional modest logo/monogram, readable channel name, optional current-program line, status. Include a visible, separately reachable Channel actions target. Card body means Watch live. Empty collections collapse; Browse channels stays reachable. |
| Guide | Provider/group/search controls above a vertical channel list. Start with 64–72dp rows: identity, optional valid current-program line, favorite/playing/unavailable status, separate Channel actions. All channels and Ungrouped are explicit choices. Prefer a group selector over a permanent third pane when a mini player is visible. |
| Mini variant | Reserve a right rail instead of covering list items: 556dp browsing content, 20dp gap, 268dp player rail. Its 16:9 video is about 268×151; identity/state and actions follow below. Home can show two 268dp cards per shelf. Preserve the focused identity and scroll context during reflow. |
| Mini actions | The video/surface expands the same session; label this Expand. Expose Stop separately. Error variants add Retry and Choose another within the rail. Give the rail an explicit D-pad entry/exit route; do not rely on a floating surface accidentally being the nearest focus target. No independent preview stream. |
| Full-screen controls | Bottom scrim, channel name first, optional reliable program title, visible playback state. Primary actions: Play/Pause when supported, Channels, Audio, Subtitles, Details, Stop. Show Return to live only when meaningful. Omit fabricated duration, seek bar and program-progress graphics for unsupported/unknown capabilities. |
| Compact channel browser | Bottom overlay; keep video visible. Favorites then Recents for the playing provider, plus All channels · Provider A. Channel identity remains usable without art or guide data. Focus does not tune; selection does. Back closes this layer before any playback cancellation/minimization rule. |
| Menus and details | Small contextual overlay, one focused action, clear title and selected values. Channel actions include favorite/hide/details; organization has explicit Finish/Cancel. Details can state Program information unavailable or Information out of date. Do not substitute skeleton cards for missing data. |

For Home cards, draw both the channel-body target and the Channel actions target. Horizontal movement should stay in the current target lane; vertical movement reaches actions and then the next shelf. The artwork must not conceal a second focus stop. For Guide rows, Right can reach that row’s actions; the mini-player route must be distinguishable from this action route. Validate the actual path with a remote before freezing geometry.

## Proposed playback mapping to test

The interaction contract deliberately leaves physical mapping open. This proposal favors Android’s playback default while retaining Fubo’s documented browse shortcut:

| Bare established playback | Result |
| --- | --- |
| OK/Center | Play/Pause when available; reveal the control state. If unavailable, reveal supported controls without pretending to pause. |
| Up | Show controls/information without pausing. |
| Down | Open compact channel browser without tuning. |
| Left/Right | Seek only if supported by the current live window; never repurpose silently as channel switching. |
| Back | Apply the contract’s first matching rule: top layer, controls/browser, start attempt, established playback, browsing/root. |

Inside visible controls/menus, OK activates the focused action. Keep Channels visible in the controls even if Down also opens it. Do not require long press for channel actions or Stop. Down-for-browser is an intentional live-TV specialization of Android’s generic information-peek mapping, not a mandated Android behavior.

## States the wireframe must make concrete

- Show a normal Home/Guide with genuinely missing program information; do not use all-rich-metadata mock data as the default.
- Show channel A in mini while browsing provider B. Expanding A and returning restores B’s browsing context; expanding never retunes or resumes A.
- Show switching to B as Connecting B, with Cancel. Failure cannot reveal A playing behind it or offer an implicit rollback.
- Show Connecting, Buffering, Reconnecting, terminal failure and Stream ended as distinct text/states. An ongoing mini failure stays mini and preserves browsing focus; actions remain reachable.
- Show the empty Favorites/Recents case, an unavailable saved channel, and an empty-after-hiding route to Manage hidden items. These are different states.
- Show paused/suspended return with an explicit valid Resume or Watch live/Return to live action, without startup autoplay.

These are acceptance-relevant product states from the interaction contract. The wireframe should expose them before adding polish. Exact focus traversal, long names, safe margins, low-contrast video backgrounds and controls at viewing distance still require real-device testing.
