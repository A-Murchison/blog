---
title: dotplasma
date: 2026-10-06
description: A Go CLI for saving, comparing, and restoring KDE Plasma desktop configuration.
tags: [go, open-source, kde, linux]
image: static/dotplasma.gif
---

`dotplasma` is a small CLI for KDE Plasma users who want their desktop configuration to be inspectable, backed up, and easy to move between machines.

It snapshots an allowlisted set of Plasma files into plain folders, so profiles can be reviewed, copied, or committed to Git without the tool doing anything surprising behind your back.

## Features

- Save Plasma profiles under `profiles/<name>/`
- Diff a saved profile against the live desktop
- Import profiles safely without applying them
- Restore profiles with `--dry-run` support and pre-restore backups
- Track only a conservative allowlist of known Plasma config files
- Keep output Git-friendly, deterministic, and under your control
- Run without root or network access

## Commands

```text
dotplasma doctor
dotplasma inspect-live
dotplasma save <profile>
dotplasma diff [profile]
dotplasma list
dotplasma import <source-dir> <profile>
dotplasma apply <profile> --dry-run
```

## Why

KDE Plasma config is powerful, but it can be messy and machine-specific. `dotplasma` focuses on a cautious workflow: save, diff, review, and only then restore if you choose to.

That makes it useful before experimenting with panels, widgets, shortcuts, desktop layouts, wallpapers, or KWin settings.

## Source

[github.com/A-Murchison/dot-plasma](https://github.com/A-Murchison/dot-plasma)
