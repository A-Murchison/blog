---
title: How MCP's work with an NBA Basketball example
date: 2026-10-22
description: how MCP (Model Context Protocol) servers work with an example using nba-mcp.
tags: [mcp, ai, nba]
image: static/options-vs-mcp.jpg
---

You may have heard the word MCP, another acronym in the AI era we're living in. This stands for Model Context Protocol.  

I'm going to break this down and give you an overview of what it is and help you understand what it is in simple terms using one I built for NBA stats.

In short, MCP is a way to give an AI a channel to invoke methods to get specific data. 

In my scenario, I query the NBA API to get live and historic statistics.

> But I can just ask ChatGPT these questions?

Yes, you can just ask ChatGPT but it will not necessarily know how to get this data reliably. 

### Without MCP

<iframe
  class="mcp-flow mcp-flow--without"
  src="static/nba-without-mcp-flow.html"
  title="How an NBA question is answered without MCP"
  loading="lazy"
></iframe>

When you ask the question: "How'd the Knicks go today?" It will look through relevant sources such as news articles, maybe Reddit forums, maybe a post on the NBA website etc. Then the AI will make a judgement based on this information. 

Although this may work for some questions, it won't give a reliable way for the AI to retrieve NBA data. You may only want the AI to retrieve the data from the NBA itself. 

### With MCP

<iframe
  class="mcp-flow"
  src="static/nba-mcp-user-flow.html"
  title="How an NBA question is answered through MCP"
  loading="lazy"
></iframe>

This is where MCP comes into play. Without MCP, the AI has to find and assess information itself; with MCP, it has a direct tool for the NBA data source.


## The details

There are four pieces in this example:

1. **You** ask Pi, “How'd the Knicks go today?”
2. **The host** is Pi: the application where you chat with the AI. It contains an MCP **client**.
3. **The NBA MCP server** offers NBA-specific tools, such as getting a game's score or a player's stats. (This may be ran locally)
4. **The NBA API** is the actual data source. The MCP server asks it for the data.

User (you), the AI (Pi), MCP server (nba-mcp), API (NBA api).

The model does not open a connection to the NBA API itself. It decides which tool could help and then the server does the actual communication. That separation lets the host control what tools are available and what they are allowed to do.

## What the AI is given

The AI is shown a small menu of tools:

- a tool name, such as `get_game_result`
- a plain English description of when to use it
- the inputs it accepts, such as a team and date

Those inputs are described with a JSON schema, effectively a contract. Clear names and descriptions matter because the model uses them to route to a given tool.

The tool menu is kept in the conversation context. The live score is fetched only when it is needed.

## 'How'd the Knicks do today? Give me a brief overview'

![How'd the Knicks go today?](static/howdtheknicksgo.jpg)

1. The model sees that a current result is needed.
2. It asks the MCP client to call the relevant tool with the team and date. 
3. The client sends that request to the NBA MCP server. (In this case get_todays_games and get_game_box_score)
4. The server checks the inputs, calls the NBA API, and formats the result.
5. The result travels back to the client and becomes available to the model.
6. The model turns the result into a useful answer: 

  > “The Knicks never lose, they beat …”

![JoshHartSideEye](static/joshhart.jpg)

### Example with JSON

For “How'd the Knicks go today?”, the model might request:

```json
{ "team": "New York Knicks", "date": "2026-10-22" }
```

The server might return structured data such as:

```json
{ "opponent": "Indiana Pacers", "knicksScore": 130, "opponentScore": 60, "status": "Final" }
```

Pi can then answer: **“The Knicks won 130–60 over the Indiana Pacers.”**


## What is happening under the hood?

MCP uses small JSON messages—structured text. When a connection starts, the client and server introduce themselves and agree on what they support. A handshake. The client can then ask for the available tools with `tools/list`, and run one with `tools/call`.

For a local server, Pi can start the process and communicate over standard input/output (`stdio`). A remote server can be reached over HTTP. Either way, the idea is the same: a request has an ID, and the server sends back the matching response.

## Security

An MCP server is a bridge to another system, so only connect servers you trust.

A read-only NBA server is relatively low risk. A server that can post to social media, spend your life savings or modify a database deserves much more care.

## Where is MCP useful?

MCP gives an AI a standard way to discover and use capabilities. It does **not** guarantee a perfect answer. The model can choose the wrong tool, misunderstand a result, or butcher the summary. The upstream API can also be delayed, incomplete, or wrong.
