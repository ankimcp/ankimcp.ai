---
title: "Install Anki MCP for Cursor, Cline & MCP Clients"
linkTitle: "MCP Clients"
description: "Configure Anki MCP with STDIO-compatible MCP clients like Cursor IDE, Cline, and Zed. Connect your AI coding assistant to Anki flashcards."
keywords: ["anki mcp cursor", "cline anki", "mcp client anki", "cursor ide flashcards", "stdio mode anki"]
weight: 2
---

This guide is for **Cursor IDE, Cline**, and other MCP clients that support STDIO. If you use Claude Desktop, see the [Desktop Installation Guide](../desktop) instead.

## What You Need

Install these first:

1. **Anki Desktop** - Your flashcard app
   Download: [apps.ankiweb.net](https://apps.ankiweb.net/)

2. **AnkiConnect Plugin** - Lets other apps talk to Anki
   Download: [ankiweb.net/shared/info/2055492159](https://ankiweb.net/shared/info/2055492159)

3. **An MCP Client** - Choose one:
   - [Cursor IDE](https://www.cursor.com/) - AI-powered code editor
   - [Cline](https://github.com/cline/cline) - VS Code extension

## Basic Configuration

All MCP clients use a similar configuration format. Choose one of the methods below:

### Method 1: Using npx (recommended - no installation needed)

Add this to your client's MCP configuration file:

```json
{
  "mcpServers": {
    "anki-mcp": {
      "command": "npx",
      "args": ["-y", "@ankimcp/anki-mcp-server", "--stdio"],
      "env": {
        "ANKI_CONNECT_URL": "http://localhost:8765"
      }
    }
  }
}
```

### Method 2: Using global installation

First, install the package globally:
```bash
npm install -g @ankimcp/anki-mcp-server
```

Then add this to your client's MCP configuration file:

```json
{
  "mcpServers": {
    "anki-mcp": {
      "command": "anki-mcp-server",
      "args": ["--stdio"],
      "env": {
        "ANKI_CONNECT_URL": "http://localhost:8765"
      }
    }
  }
}
```

## Client-Specific Setup

### Cursor IDE

**Configuration File Location:**
- macOS/Linux: `~/.cursor/mcp.json`
- Windows: `%USERPROFILE%\.cursor\mcp.json`

**Steps:**
1. Create or edit the configuration file
2. Add the basic configuration from above
3. Save and restart Cursor IDE

### Cline (VS Code Extension)

**Configuration:**

Cline has a built-in settings UI for managing MCP servers:
1. Open VS Code
2. Open Cline extension
3. Click "Configure MCP Servers"
4. Add the basic configuration from above
5. Save and restart VS Code

**Alternative:** Edit `cline_mcp_settings.json` directly with the basic configuration.

**Windows users**: If you encounter `spawn npx ENOENT` errors, use `"command": "cmd"` with `"args": ["/c", "npx", "-y", "@ankimcp/anki-mcp-server", "--stdio"]`

## Try It Out

After configuration, restart your MCP client and try:

**Create a flashcard:**
```
You: "Create an Anki flashcard with 'What is MCP?' on the front and
'Model Context Protocol - a standard for AI assistants to connect to
external tools' on the back"
```

**List your decks:**
```
You: "Show me my Anki decks"
```

**Start a review session:**
```
You: "Let's review my Spanish deck"
```

## Troubleshooting

### "Command not found: npx"

Install Node.js from [nodejs.org](https://nodejs.org/). The npm package manager (which includes npx) comes with Node.js.

### "Cannot connect to AnkiConnect"

1. Make sure Anki is running
2. Verify AnkiConnect plugin is installed (Tools → Add-ons)
3. Check that AnkiConnect is using port 8765 (default)
4. If using a different port, update the `ANKI_CONNECT_URL` in your configuration

### "spawn npx ENOENT" (Windows + Cline)

This is a common Windows issue. Use the Windows-specific configuration with `cmd /c`:

```json
{
  "mcpServers": {
    "anki-mcp": {
      "command": "cmd",
      "args": ["/c", "npx", "-y", "@ankimcp/anki-mcp-server", "--stdio"]
    }
  }
}
```

### Server not appearing in client

1. Check that your configuration JSON is valid (no trailing commas, proper quotes)
2. Restart your MCP client after configuration changes
3. Check client logs for error messages

## Advanced Configuration

### Custom AnkiConnect URL

If your AnkiConnect runs on a different port or computer:

```json
{
  "mcpServers": {
    "anki-mcp": {
      "command": "npx",
      "args": ["-y", "@ankimcp/anki-mcp-server", "--stdio"],
      "env": {
        "ANKI_CONNECT_URL": "http://192.168.1.100:8765"
      }
    }
  }
}
```

## Need Help?

- [GitHub Discussions](https://github.com/ankimcp/anki-mcp-server/discussions) - Ask questions and share tips
- [Discord Server](https://discord.gg/JVNcxNB3e7) - Chat with the community
- [Email Support](mailto:support@ankimcp.ai) - Direct support

Happy learning! 📚
