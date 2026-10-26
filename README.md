<div align="center">

<img src="assets/hero.png?v=6" alt="ORBT: album cover and waveform in the macOS menu bar" width="100%">

<img src="assets/icon.png" width="128" alt="ORBT icon">

# ORBT

**Your album cover in the macOS menu bar, with a waveform next to it.**

[![macOS](https://img.shields.io/badge/macOS-14.2%2B-black?logo=apple&logoColor=white)](#install)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![Download](https://img.shields.io/github/v/release/Daniil15DDD/ORBT?label=download)](https://github.com/Daniil15DDD/ORBT/releases/latest)
[![Ko-fi](https://img.shields.io/badge/Ko--fi-Support%20me-FF5E5B?logo=ko-fi&logoColor=white)](https://ko-fi.com/barabashka123)

</div>

## Why

macOS shows a plain icon for Now Playing. ORBT shows the **real cover** instead, like the iPhone's Dynamic Island. Click it for a small player.

<div align="center">
<img src="assets/menubar-playing.png" width="560" alt="Playing">
<br>
<img src="assets/menubar-paused.png" width="560" alt="Paused">
<br><sub>Playing · Paused</sub>
<br><br>
<img src="assets/popover.png?v=6" width="360" alt="The player popover">
</div>

## On the lock screen

A player card sits above the macOS lock screen: cover, title, seek bar, shuffle / previous / play / next / repeat and a favourite star. Click the small cover for fullscreen: a big cover with a soft colour wash, or, when Apple has made **moving artwork** for the album, the video fills the whole screen.

<div align="center">
<img src="assets/lockscreen-fullscreen.png?v=7" width="720" alt="Lock screen fullscreen with the big cover and the player card">
<br><sub>Static cover: the big cover with a colour wash and the Liquid Glass clock.</sub>
<br><br>
<img src="assets/lockscreen-moving.png?v=7" width="720" alt="Lock screen fullscreen with Apple's moving artwork filling the screen">
<br><sub>Moving artwork: the video fills the screen (a still frame is shown here).</sub>
<br><br><sub>Captured from the app's own views (the real lock screen shows your wallpaper behind the card).</sub>
</div>

**Your own clock.** Fullscreen draws its own clock: pick a font (serif, sans, rounded, mono, or your own fonts), a weight and a size in Settings, or **long-press the clock** to change its size and turn on **Liquid Glass digits**, with a slider from clear glass to fully lit glass. Text and buttons switch to the cover's own colour on bright covers so they stay readable.

<div align="center">
<sub>In fullscreen, two buttons in the bottom-right corner open <b>lyrics</b> (time-synced, the current line big and bright, tap a line to jump there) or the <b>queue</b>. Either button can be hidden in Settings.</sub>
</div>

<div align="center">
<img src="assets/lockscreen-lyrics.png?v=7" width="720" alt="Lock screen lyrics view with the cover and player card on the left and synced lyrics on the right">
<br><br>
<img src="assets/lockscreen-queue.png?v=7" width="720" alt="Lock screen queue view listing the next songs">
<br><sub>Both images use placeholder text, not real lyrics or songs.</sub>
</div>

## Features

- Real album art and an animated waveform in the menu bar
- Compact player: seek bar, previous / play / next, shuffle, repeat
- **Lock screen player** with a fullscreen mode and Apple's **moving artwork** (when the album has it)
- **Lyrics** and **queue** on the fullscreen lock screen, each with a button you can hide in Settings
- **Custom lock screen clock**: font, weight, size and Liquid Glass digits (long-press the clock to edit)
- Favourite (star) and equalizer presets for Apple Music; the lock screen card uses a Liquid Glass look by default (switch to a frosted look in Settings)
- Works with **Apple Music** and **Spotify** (Spotify's real queue and a save button need an optional one-time connection, see below)
- Light on resources (about 1% CPU while playing), no Dock icon, no audio recording

## Performance

Built to stay out of the way. Measured with `top` on an Apple Silicon MacBook (macOS 27) while a song was playing, with the popover and lock screen closed:

<div align="center">
<img src="assets/performance.png?v=6" width="720" alt="About 1% CPU while playing, under 1% while paused, about 100 MB memory">
</div>

How: the waveform animates on the graphics side, the menu bar uses a small thumbnail of the cover, updates come from Music's own notifications, and the moving-artwork video is only buffered while the Mac is locked (about +25 MB while it plays; the CPU and memory numbers above were not re-measured with it playing). The memory figure was measured with `top` after launch and includes the lock screen windows (about 24 MB of it).

## Install

1. Download the zip from [Releases](https://github.com/Daniil15DDD/ORBT/releases/latest) and unzip it.
2. Move `ORBT.app` to Applications and right-click → **Open** (it is not notarized).
3. Allow it to control Music and Spotify when macOS asks.

Needs macOS 14.2+. To build it yourself instead: `git clone` this repo, then `./build.sh` (Command Line Tools are enough).

## Good to know

- The waveform is a lively animation, not a real audio analysis, so nothing is listened to. An optional setting makes it react to live audio (macOS then asks for audio-capture permission).
- The equalizer is Apple Music only. Spotify's scripting interface has no like command and no queue, so those use Spotify's Web API, which is optional: create a free Spotify developer app (its owner needs Premium; Spotify limits such apps to 5 users), add the redirect URI `http://127.0.0.1/callback`, paste its Client ID in Settings and log in once. ORBT keeps the token in the Keychain. This is untested against a real Spotify account so far.
- Lyrics come from [LRCLIB](https://lrclib.net), a free open database: it receives the song title, artist, album and length. Not every song has them.
- The queue shows the next songs of the current Apple Music playlist. With shuffle on, Apple Music doesn't share what plays next, so "Recently played" is shown instead.
- The lock screen player uses undocumented macOS window calls, because Apple offers no official way to draw there. A macOS update could break it. Turn it off in Settings if you prefer.
- Moving artwork is read from Apple's public catalogue pages, which is unofficial. When an album has none, you get the normal cover.
- No song info? Check System Settings → Privacy & Security → Automation.

## Support

If you like it, you can support me on Ko-fi, and a star helps others find it.

[![Support me on Ko-fi](https://img.shields.io/badge/Support%20me%20on-Ko--fi-FF5E5B?style=for-the-badge&logo=ko-fi&logoColor=white)](https://ko-fi.com/barabashka123)

MIT licensed. Inspired by iOS Now Playing and [Boring Notch](https://github.com/TheBoredTeam/boring.notch); no code copied. Album artwork shown in the images belongs to its owners.
