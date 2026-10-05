# Live pause, rewind, and temporary buffering

Research date: 2026-10-04. Product discovery evidence, not an implementation decision. Scope: the first Android TV release, live TV through Xtream Codes connections, with saved recordings and DVR workflows deferred.

## What the stream already provides

For adaptive live playback such as HLS/DASH, Media3 describes a moving window of available media. Seeking is within that window, and returning to its default position normally moves near live. A long pause or buffering interruption can leave playback behind the available window; resuming at the old position can then fail. Progressive live streams do not expose that adaptive live window. This does **not** mean their picture cannot be paused; it means that a seekable broadcast history is not supplied through that model. [Media3 live streaming](https://developer.android.com/media/media3/exoplayer/live-streaming)

The delivery format matters. Media3 supports MPEG-TS both inside HLS and as a progressive container, so “TS channel” alone does not establish rewind support. Playability also depends on supported audio/video formats. [Media3 supported formats](https://developer.android.com/media/media3/exoplayer/supported-formats)

In HLS, the media playlist identifies segments and durations; the server may remove older segments from a live playlist. **Inference:** this availability is independent of an electronic program guide. Missing titles or broadcast schedules therefore cannot establish whether rewind exists, and useful guide data cannot establish that old video is available. [HLS specification, media segments and live playlists](https://www.rfc-editor.org/rfc/rfc8216.html#section-6.2.2)

## Pause and guaranteed resume are different promises

Media3 exposes play/pause separately from seeking. `pause()` changes the intention to play; it does not promise to retain everything broadcast during the interruption. The Player API separately reports whether the current item is seekable and which commands are currently available. Those commands can change. **Product inference:** show controls from actual playback capabilities, update them when capabilities change, and avoid implying that a visible Pause button guarantees same-place resume after any length of absence. [Media3 Player contract](https://developer.android.com/reference/androidx/media3/common/Player)

Media3 provides ordinary buffering controls, including maximum forward-buffer duration and retention of previously played media for faster backward seeks. These are useful player mechanisms, not evidence that setting a buffer value creates a complete DVR for arbitrary inputs. A usable temporary-buffer feature still needs a defined retained interval and demonstrated pause/resume/seek behavior. [DefaultLoadControl.Builder](https://developer.android.com/reference/androidx/media3/exoplayer/DefaultLoadControl.Builder), [LoadControl](https://developer.android.com/reference/androidx/media3/exoplayer/LoadControl)

## Keep three product concepts separate

- **Existing live rewind:** use the history currently exposed by the playing source. Its limits are discovered during playback, rather than promised for every channel.
- **Temporary local time-shifting:** retain incoming video on the TV for the current viewing session, allowing replay of received footage within a bounded interval. Android's TV-input guidance treats this as temporary recording with storage management, an advancing oldest position, and cleanup when the session ends. This source explains the concept; it is not a recommendation to adopt TV Input Framework or proof that Media3 supplies automatic local time-shifting. [Android TV time-shifting](https://developer.android.com/training/tv/tif/time-shifting)
- **Saved recording or provider catch-up:** saved recording retains content for later sessions; use “provider catch-up” here to mean access to earlier broadcasts supplied by the provider. Neither should be inferred from a live rewind control. Saved recording remains deferred; actual provider archive access is unverified. Android likewise distinguishes session time-shifting from recording for later viewing. [Android TV time-shifting and recording distinction](https://developer.android.com/training/tv/tif/time-shifting)

## Recommended next question

**For the first release, should pause and rewind use what each channel already supports, or should the app also keep a temporary buffer on the TV?**

- **A — Use available channel controls (recommended):** offer pause/rewind where playback supports them, within their actual limits; defer a dedicated temporary buffer.
- **B — Add a temporary TV buffer:** make bounded pause/rewind of received video a first-release feature, including compatible streams that lack their own rewind window.

A keeps the initial commitment focused. B is a valid feature choice, but needs subsequent decisions about buffer length, when buffering starts, channel-change behavior, and storage exhaustion. Neither option guarantees every provider behaves alike. No actual provider streams or Android TV devices were tested here; reliable resume duration and local-buffer compatibility remain unproven.
