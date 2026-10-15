# Spotify Media for Niri

A Niri-adjusted fork of [Spotify Media](https://noctalia.dev/plugins/community/spotify-media), the compact Noctalia bar widget with album artwork, scrolling track information, playback controls, and Spotify launch/focus behavior.

## Plugin

| Field   | Value                   |
| ------- | ----------------------- |
| ID      | `question44/spotify-media-niri` |
| Entries | Bar widget: `bar`       |

## Requirements

The following dependencies must be installed and available on `PATH`:

* `playerctl` — reads Spotify MPRIS metadata and controls playback.
* `niri` — detects and focuses an existing Spotify window through Niri IPC.
* `spotify-launcher` — launches Spotify when it is not already running.

Playback metadata and controls use the Spotify MPRIS player name `spotify`. Window matching uses Niri's `app_id` and matches IDs containing `spotify`, including `com.spotify.Client`.

## Usage

Enable `question44/spotify-media-niri` in Noctalia and add its `bar` widget to a Noctalia bar.

When Spotify is running, the widget displays:

* Album artwork
* Continuously scrolling `Artist – Title`
* Previous track
* Play / pause
* Next track

Hovering over the track text shows the full track information in a tooltip.

Click the album artwork or track text to open Spotify:

* If Spotify is already running, the existing Spotify window is focused.
* If Spotify is not running, `spotify-launcher` is started.

When Spotify is closed, the widget collapses to a Spotify icon.

## Notes

The widget uses `playerctl --player=spotify` to read metadata and send playback commands.

Spotify window detection is performed with:

```text
niri msg --json windows
```

An existing Spotify window is focused with:

```text
niri msg action focus-window --id <window-id>
```

If no Spotify window is found, the plugin spawns:

```text
spotify-launcher
```

Album artwork URLs are obtained from Spotify's MPRIS metadata. Remote artwork is downloaded into the plugin data directory and cached using two alternating cover image files.

The widget polls metadata approximately once per second. The marquee animation updates separately at a 250 ms interval.

The widget is Spotify-specific and uses Niri for window focus.

## Fork attribution

This project is based on `azokyen/spotify-media` from the Noctalia community plugin collection. The playback widget and artwork handling are retained; the plugin ID, manifest, documentation, and window focus behavior are adjusted for Niri.
