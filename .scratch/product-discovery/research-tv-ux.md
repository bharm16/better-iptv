# Live-TV UX: Fubo, Sling, and YouTube TV

Researched and revised: 2026-10-04. Scope: living-room interfaces for an Android TV-first IPTV player. Fubo, Sling, and YouTube TV are the primary analogues; cable services and Google TV provide supporting examples. Sources are official product help, product/design announcements, and Android guidance. This is research and a design recommendation, not an accepted layout or implementation specification.

## Finding

Fubo, Sling, and YouTube TV are useful primary analogues because they combine live television, program discovery, and personal collections. They preserve distinct Home, guide, and saved-content functions while adding shortcuts across them. Fubo's documentation puts favorites in both Home and Guide; Sling brings channel browsing into playback; YouTube TV combines personalized Home with a customizable Live guide. [Fubo favorites](https://support.fubo.tv/hc/en-us/articles/360028439511-How-do-I-Favorite-the-channels-I-watch-most), [Sling player redesign](https://www.sling.com/whatson/announcements/new-features), [YouTube TV](https://support.google.com/youtubetv/answer/7067974/watch-shows-sports-events-amp-movies).

There is no universal Home/Guide layout in the evidence. The user's complaint is better expressed as a continuity requirement: familiar channels, preferences, and browsing context should remain useful across visits. A combined screen can still fail if it resets to the first channel; a separate Home can work if it shares personal state with the guide. The integrated design proposed below is a hypothesis to test, not a proven winner.

## Primary comparison

| Viewing task | Fubo | Sling | YouTube TV |
| --- | --- | --- | --- |
| **Find something to watch now** | Home presents live/upcoming programming and recommendations. Guide provides the channel schedule; Sports provides another route by event. [TV interface](https://support.fubo.tv/hc/en-us/articles/115003421412-Connected-Device-Smart-TV-User-Interface). | The 2021 redesign introduced a recommendation-focused Home and separate Guide. Current help still identifies Home and Guide with a shared left menu. [2021 launch](https://www.sling.com/sling-newsroom/posts/pressreleases/sling-tv-unveils-new-app-experience-deliverin), [Current navigation help](https://www.sling.com/help/en/learn-about-sling/rentals-vod). | Home recommends programs using YouTube TV/YouTube viewing history. Live shows current programs by network. Personalization also reaches the guide; see the design note below. [Watching help](https://support.google.com/youtubetv/answer/7067974/watch-shows-sports-events-amp-movies). |
| **Keep familiar channels accessible** | Explicit channel favorites appear at the beginning of Home and Guide. Reordering on a supported device applies across devices; profiles have their own favorites. [Favorites](https://support.fubo.tv/hc/en-us/articles/360028439511-How-do-I-Favorite-the-channels-I-watch-most), [Ordering](https://support.fubo.tv/hc/en-us/articles/360034716932-Can-I-reorder-my-Favorites), [Profiles](https://support.fubo.tv/hc/en-us/articles/360041877712-How-do-Profiles-work-on-Fubo). | The guide exposes channel favorites and category navigation. Profiles have their own favorites, recommendations, and watchlists. The help does not explain how recommendation ranking is computed. [Guide](https://www.sling.com/help/en/learn-about-sling/using-sling/guide), [Profiles](https://www.sling.com/help/en/learn-about-sling/using-sling/user-profiles). | Viewers can explicitly hide and reorder networks; those preferences follow them across devices. This control is distinct from history-based recommendations. [Live guide preferences](https://support.google.com/youtubetv/answer/7067974/watch-shows-sports-events-amp-movies). |
| **Return to saved or unfinished programs** | My Stuff separates Recordings, Watchlist, Continue Watching, and Scheduled Recordings. Continue Watching offers Resume or Play from start. [My Stuff](https://support.fubo.tv/hc/en-us/articles/5473150198797-What-is-My-Stuff). | DVR is the recordings destination; on-demand browsing is separate. The 2025 player redesign offers Resume/Restart when available. [DVR help](https://www.sling.com/help/en/troubleshooting/dvr-help), [Player announcement](https://www.sling.com/whatson/announcements/new-features). | Library organizes recorded and scheduled programs. It is a different job from browsing what is live now. [Library help](https://support.google.com/youtubetv/answer/7067974/watch-shows-sports-events-amp-movies). |
| **Browse while watching / return to a channel** | On TV devices, Down opens Browse While Watching; Left/Right browses current programs, Down again exposes genre filters. OK switches channel; Back closes the browser and keeps the current channel. [TV browsing controls](https://support.fubo.tv/hc/en-us/articles/360002868712-How-can-I-browse-other-programming-while-watching-my-current-channel). | The 2025 player announcement places Recent/Favorite Channels near player controls and describes Browse and Watch. Current TV help confirms holding Select returns to the previous channel. [Announcement](https://www.sling.com/whatson/announcements/new-features), [TV controls](https://www.sling.com/help/en/learn-about-sling/using-sling/player-controls). | Holding OK/Select returns to the last channel. This confirms channel recall, not a complete guarantee of where guide focus returns. [Remote tip](https://support.google.com/youtubetv/answer/7067974/watch-shows-sports-events-amp-movies). |
| **Launch and return after leaving** | Profiles help documents a Who's Watching entry screen. No complete cold-start, autoplay, or guide-position restoration contract was established by the reviewed sources. [Profiles](https://support.fubo.tv/hc/en-us/articles/360041877712-How-do-Profiles-work-on-Fubo). | No current, platform-complete startup or focus-restoration policy was established. Undated Android marketing uses My TV while current help says Home; that does not settle the current Android TV landing layout. [Android marketing](https://www.sling.com/supported-devices/android). | TV startup autoplays a top recommendation unless Autoplay on Start is disabled. The documented behavior does not promise the last watched channel or saved guide position. [Startup setting](https://support.google.com/youtubetv/answer/7067974/watch-shows-sports-events-amp-movies). |

**Evidence boundaries:** Fubo's general TV and favorites articles are from May 2024; they include Android TV and warn of device variations. [Apple TV help updated 2026-03-02](https://support.fubo.tv/hc/en-us/articles/43790283314061-How-do-I-watch-Fubo-on-my-Apple-TV) corroborates Home/Guide/My Stuff and favorites at the guide's top, but is not proof of Android TV parity. Its Browse While Watching article is dated 2025-03-11; My Stuff is dated 2025-06-10. Sling's current guide help explicitly separates a newer **Roku** guide from other experiences; its 2025 player announcement was Roku-first. Current Sling and YouTube help pages provide no visible publication date. Historical design announcements establish intent and precedent, not an exact current screenshot for every device.

## The design evidence that matters

YouTube TV's Head of Design describes in-home interviews, feedback, surveys, and concept testing that found decision fatigue and demand for quick access to familiar, currently relevant programming. The 2023 redesign put curated recommendations **at the top of the live guide**, made the grid compact, improved program information, and added contextual side actions. Home, Live, and Library remained distinct. This is direct precedent for combining discovery with a schedule. [YouTube design account, 2023-01-18](https://blog.youtube/news-and-events/youtube-tv-live-guide-and-library/).

Fubo provides a practical constraint: its support team acknowledges that missing keywords can prevent a game from appearing on the Sports screen, and directs viewers to the channel guide. Therefore event discovery should supplement, rather than become the only way to reach, a channel. [Fubo missing-game guidance, 2025-10-02](https://support.fubo.tv/hc/en-us/articles/360015388351-Your-website-says-you-re-showing-my-game-but-I-can-t-find-the-channel).

The combined lesson is a design inference: **put personal usefulness wherever viewing decisions happen**. Keep explicit favorites stable, label inferred recommendations separately, and let viewers browse without switching away from their current program merely by moving focus. A large recommendation engine is not necessary to implement recent channels and favorites well.

## Supporting examples

- **DIRECTV on TV devices:** Your TV combines recent channels and recommendations, with a separate Guide, a ten-channel recents overlay, and Home-versus-last-channel startup preference. [Your TV](https://www.directv.com/support/article/000101737).
- **Xfinity X1 set-top boxes:** Saved/For You, Last Watched, and a right-side mini-guide complement the full guide. These are not Xfinity Stream app claims. [Main menu](https://www.xfinity.com/support/articles/x1-guide-main-menu-overview), [Last Watched](https://www.xfinity.com/support/articles/x1-last-watched), [Mini-guide](https://www.xfinity.com/support/articles/x1-guide-how-to-navigate-in-the-mini-guide).
- **Google TV's US system Live/Freeplay guide:** favorites sit at the top; Recents is another guide section and requires Web & App Activity. This does not promise integration for arbitrary third-party apps. [Google TV](https://support.google.com/googletv/answer/11167990?hl=en).
- **Spectrum on Roku:** a device-specific startup preference chooses a channel or returns to the last watched one. Evidence was retrieved from the official page's search index; direct opening returned HTTP 403. [Roku settings](https://www.spectrum.net/support/tv/new-spectrum-tv-app-roku-settings).

These sources establish documented or advertised behavior, not comparative usability or reliability. No paid accounts, credentials, or hands-on competitor sessions were used.

## Standards versus conventions

Android's actual baseline is remote usability: few clicks and screens, predictable directional movement and Back behavior, and a clearly focused action on launch or while idle. Home on the physical remote goes to the **system** home. Basic functionality must work with D-pad, Select, and Back rather than depending on specialized cable-remote keys. The guide also describes a fixed app start destination; it does not mandate that this destination be a channel grid. Its special direct-Back behavior for Google TV Live-tab launches applies to that integration path. [Android TV navigation, updated 2026-09-08](https://developer.android.com/training/tv/get-started/navigation).

Android distinguishes focused, pressed, and selected states. For this app, a channel being browsed and a channel currently playing should therefore remain visually distinct. This last sentence is our application of the guidance. [Focus system, updated 2024-03-21](https://developer.android.com/design/ui/tv/guides/styles/focus-system).

Android's component guidance supports tabs for peer content; its layouts favor readable, grouped content, predictable row navigation, and overlays that retain the underlying context. Those tools support either adjacent Home/Guide views or a compact personal section above a grid. They do not decide between them. [Tabs, updated 2026-03-30](https://developer.android.com/design/ui/tv/guides/components/tabs), [Layouts](https://developer.android.com/design/ui/tv/guides/styles/layouts).

## The state contract matters more than the startup label

The X1 default-guide article explicitly distinguishes a saved default, a temporary session filter, and a main-menu entry path that opens All Channels. That is a useful warning: adding Favorites is insufficient if a route bypasses it. We should define behavior for every entry and return route, rather than copying that inconsistency. [X1 default guide](https://www.xfinity.com/support/articles/x1-default-guide-view).

The following is a **proposed contract to validate**, not behavior proven across the researched apps:

| Situation | Proposed behavior |
| --- | --- |
| App restart or device restart | Keep favorites, their order, recent channels, and personal preferences. The home view uses that history immediately when available. |
| Open playback from Home or Guide, then return during the session | Return to the originating view, category/filter, and relevant focused item; retain scroll context when that item still exists. |
| Move between Home and Guide | Share the same favorites and channel identities; avoid two independent lists that drift. Provide a direct route into the guide around the selected or playing channel. |
| Reopen after a long absence | Keep personal data, refresh schedule information, and bring live browsing back to **Now** rather than presenting yesterday's time range as current. The threshold for a long absence remains undecided. |
| Data refresh removes the focused channel or program | Move focus to a stable, visible alternative in the same context. Do not silently jump to the first channel while the viewer is navigating. Exact fallback order needs a prototype. |
| Return to a recent live channel | Tune to what is live on that channel now. Present the current program if trustworthy metadata is available. Do not imply the earlier program can resume from a saved position. |

None of the competitor help pages inspected provide a complete guarantee for restoring both focus and scroll after playback, process death, and schedule updates. Those behaviors remain our own requirements to design and test.

## Live-channel return is different from resuming a program

Fubo documents separate options for watching an in-progress recording live or from its beginning, with Go to Live available when behind. Its Lookback documentation describes replay availability up to 72 hours and shows expiration information for events. These are service-backed playback capabilities. [In-progress recording, updated 2025-04-21](https://support.fubo.tv/hc/en-us/articles/8361914566029-How-can-I-watch-an-in-progress-Cloud-DVR-recording), [Lookback, updated 2025-04-22](https://support.fubo.tv/hc/en-us/articles/115000414712-What-is-Lookback).

Sling's help says channels without certain player controls may only be available live, and ad-skipping capability varies with channel-provider agreements. Therefore a remembered channel and a remembered playback position must not be treated as interchangeable capabilities. [Sling player controls](https://www.sling.com/help/en/learn-about-sling/using-sling/player-controls).

For the proposed IPTV app, use **Recent channels** or **Back to [channel]** for returning to live television. Reserve **Continue watching**, **Restart**, and historical program playback for content whose actual playback capability has been verified. This is a product recommendation. The sources above do not document Xtream-compatible server behavior; protocol, archive support, stream limits, and metadata quality require separate investigation against the intended services.

## Recommendation for this app

Prototype **one Live TV landing screen with a compact personal section connected directly to the full guide** first. Prioritize recent channels and favorites, with current program information where available; retain an obvious path to all channels. Keep this section compact enough that the schedule remains useful from the couch. This is a proposed response to the user's complaint, not a layout decision already accepted.

Compare it with **adjacent Home and Guide views sharing the same personal state**. The integrated option may reduce view switching but consume guide space; adjacent views preserve more space for each task but add a switch. Both should offer a lightweight channel browser during playback and preserve the return context. The research supports the ingredients; remote testing must establish the arrangement and control mapping.

The first prototype should compare these two layouts on the same tasks: return to a familiar channel, inspect what is on favorite channels, explore an unfamiliar channel, switch while a program continues, and return from playback to the item being browsed. Test a restart and a program-boundary update too. Attractive static screens will not resolve the user's central complaint if state disappears during those transitions.

## Fallbacks and remaining decisions

The following are proposed resilience rules, not claims about what every provider supplies:

- **No viewing history:** show available channels and a short, optional route to choose favorites. Do not manufacture a personalized row or require setup before watching.
- **No favorites:** keep recent channels usable and make favoriting available at the channel. Hide empty shelves rather than filling the screen with placeholders.
- **Missing program metadata:** keep a usable channel tile/row, identify the channel, and say program information is unavailable. A missing schedule does not, by itself, establish that the stream is unavailable.
- **Stale schedule:** distinguish stale information from current programming and refresh it without moving focus unexpectedly. Do not invent a title, progress indicator, genre, or artwork.
- **No usable artwork:** use a readable text/channel fallback; the personal view must not depend on a poster catalog.
- **Removed or unavailable channel:** preserve a comprehensible place in the personal view long enough to explain the failed selection and offer another choice; exact retention behavior is open.
- **No verified catch-up or resume capability:** returning to the channel means live playback. Do not offer controls whose outcome cannot be supported by the connected service.

The next user decision is the relationship between Home and Guide: adjacent views in one Live TV area, a personal band above the grid, or a more separate Home page. After that, resolve whether Home is quiet or starts video; whether the viewer's explicit favorites or recent viewing comes first; the minimal remote controls; and whether personal data belongs to the device, a household, or an individual profile. These choices remain open. No framework, account system, provider protocol, cloud sync, recommendation engine, or DVR implementation is selected by this research.
