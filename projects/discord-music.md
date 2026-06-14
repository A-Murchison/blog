---
title: discord-tunes
date: 2026-06-14
description: A Discord music bot that streams YouTube and Spotify into voice channels.
tags: [go, open-source, discord]
---

A Discord bot that plays music in voice channels. Streams from YouTube URLs or Spotify, queues tracks, and skips when you're done with a song.

Built in Go, using FFmpeg and yt-dlp under the hood.

## Commands

- `!play <url>` - add a track and start playing
- `!skip` - skip the current track
- `!stop` - stop and clear the queue
- `!clear` - clear the queue, keep playing
- `!diag` - check FFmpeg, libopus, and yt-dlp status

## Source

[github.com/A-Murchison/discord-tunes](https://github.com/A-Murchison/discord-tunes)
