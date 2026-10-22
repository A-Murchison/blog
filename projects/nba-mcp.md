---
title: nba-mcp
date: 2026-10-21
description: An MCP server that gives AI assistants live NBA scores, box scores, rosters, and stats.
tags: [typescript, mcp, nba, open-source]
image: static/knicks-recap.gif
---


`nba-mcp` is a [Model Context Protocol](https://modelcontextprotocol.io/) server that gives AI assistants access to NBA data. Connect it to an MCP client and ask natural-language questions about live games, scores, box scores, play-by-play, team rosters, and player or team statistics.

It supports a deterministic mock provider for development and a public NBA.com provider for current game and season data. No API key is required.


## What it can do

- Find games that are live now, scheduled today, or happening this week
- Check a game's score, period, clock, box score, and recent events
- Look up team rosters and search for teams or players
- Retrieve player and team season statistics and game logs
- Browse league leaders, standings, and selected historical game data

### Examples
In the header gif, I asked the AI:
- "How'd the Knicks do today? Give me a brief overview"

Other examples you can ask your AI:
- “What NBA games are live right now?”
- “What is the score of the Lakers game?”
- “Who is leading this game in points?”
- “Who is on the Boston Celtics roster?”

## Built with

TypeScript, Bun, and the [Model Context Protocol TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk). The server communicates over standard input/output, so it works with MCP clients such as Pi, Claude Desktop, and Visual Studio Code.

## Source

[github.com/A-Murchison/nba-mcp](https://github.com/A-Murchison/nba-mcp)
