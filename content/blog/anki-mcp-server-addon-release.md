---
title: "Anki MCP Addon: Native AI Integration Without AnkiConnect"
date: 2025-12-05
author: "Anatoly"
author_link: "https://anatoly.dev"
description: "Install the Anki MCP addon for direct AI assistant integration. No Node.js, no AnkiConnect, no external servers - the MCP server runs natively inside Anki."
keywords: ["anki mcp addon", "native anki mcp", "anki ai integration", "claude anki addon", "mcp server addon"]
categories: ["releases"]
tags: ["addon", "anki", "native", "mcp server"]
sitemap_priority: 0.8
---

Stop switching between terminals just to use AI with Anki. The **Anki MCP addon** runs an MCP server directly inside Anki - install once, connect your AI assistant, done.

## Why a Native Anki MCP Addon?

Using AI with Anki previously meant:

- Installing Node.js
- Running a separate server process
- Keeping AnkiConnect installed
- Managing multiple terminal windows

The Anki MCP addon eliminates all of this. One addon install, zero external dependencies.

## How the Addon Works

The MCP server runs in a background thread inside Anki. When Anki starts, the server starts. When Anki closes, it shuts down cleanly.

```
AI Assistant (Claude Desktop)
         ↓
    HTTP (port 3141)
         ↓
   AnkiMCP Server (inside Anki)
         ↓
   Your Collection
```

No middleman. Your AI talks directly to Anki.

## Installation

### From AnkiWeb (recommended)

1. In Anki: *Tools → Add-ons → Get Add-ons...*
2. Enter code: **124672614**
3. Restart Anki

The server starts automatically on `http://127.0.0.1:3141/`.

### From GitHub

Download `.ankiaddon` from [Releases](https://github.com/ankimcp/anki-mcp-server-addon/releases) and double-click to install.

## Connect Claude Desktop

Add to your config file (`~/Library/Application Support/Claude/claude_desktop_config.json` on macOS):

```json
{
  "mcpServers": {
    "anki": {
      "url": "http://127.0.0.1:3141/"
    }
  }
}
```

Restart Claude Desktop. You're connected.

## Tunnel Support

Need to access Anki remotely? The addon works out of the box with Cloudflare Tunnel, ngrok, and similar tools. Point your tunnel to `http://127.0.0.1:3141/` and connect from anywhere.

This means you can use Claude.ai, ChatGPT, or any web-based AI assistant with your local Anki - no npm package required.

## What You Can Do

The Anki MCP addon exposes 27 tools across these categories:

**Collection Management**
- Sync with AnkiWeb
- List, create, and manage decks

**Notes & Cards**
- Search using Anki's query syntax
- Create, edit, and delete notes
- Get detailed note information

**Review Sessions**
- Get due cards
- Present card content
- Rate cards (Again/Hard/Good/Easy)

**Note Types**
- List and inspect models
- Create new note types
- Update CSS styling

**Media**
- Store images and audio
- List and delete media files

**GUI Integration**
- Open browser with search
- Launch add cards dialog
- Edit specific notes

## Requirements

- **Anki 25.x or later** (uses Python 3.13)

That's it. No Node.js, no npm, no AnkiConnect.

## Configuration

Default port is 3141. To change it:

*Tools → Add-ons → AnkiMCP Server → Config*

```json
{
  "http_port": 3141,
  "http_host": "127.0.0.1",
  "auto_connect_on_startup": true
}
```

Restart Anki after changing port.

## Troubleshooting

**Server not starting?**
- Check *Tools → AnkiMCP Server Settings...* for status
- Verify Anki 25.x (older versions won't work)

**Port already in use?**
- Change port in addon config (see above)
- Or stop other services using 3141

**Claude Desktop not connecting?**
- Verify config JSON syntax
- Restart both Anki and Claude Desktop
- Check URL matches your port setting

## Addon vs npm Package

Both options remain available:

| Use Case | Recommendation |
|----------|----------------|
| Simplest setup | **Anki MCP Addon** |
| Cursor, Cline (STDIO) | npm package with `--stdio` |
| ChatGPT, Claude.ai (web) | npm package with `--ngrok` |

## Get Started

**[Install from AnkiWeb →](https://ankiweb.net/shared/info/124672614)**

Or enter code `124672614` in *Tools → Add-ons → Get Add-ons...*

## Links

- [AnkiWeb Page](https://ankiweb.net/shared/info/124672614)
- [GitHub Repository](https://github.com/ankimcp/anki-mcp-server-addon)
- [Report Issues](https://github.com/ankimcp/anki-mcp-server-addon/issues)

More features coming as development continues.

---

{{< newsletter >}}
