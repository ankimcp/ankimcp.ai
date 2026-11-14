---
title: "Anki Studio Reference"
linkTitle: "Anki Studio"
description: "Reference for AnkiMCP's Anki Studio: every MCP tool the Studio server exposes to your AI assistant, grouped by feature, and where to find the Studio MCP URL."
keywords:
  - AnkiMCP Studio reference
  - Anki Studio MCP tools
  - Studio MCP tools list
  - ankimcp studio tools
  - anki studio reference
weight: 2
sitemap_priority: 0.7
---

**This section documents Anki Studio — AnkiMCP's cloud side, which your AI reaches through the Studio MCP endpoint.** It's a lookup section, not a tutorial: exact names, exact behaviour.

Studio is separate from the tunnel to the Anki on your computer. The tools your AI uses to work with your local decks — through the [AnkiMCP add-on](/docs/reference/addon/) or the CLI — are documented separately, and nothing on these pages describes them. If you're not sure which of those you have, see [Add-on vs CLI](/docs/concepts/add-on-vs-cli/).

## Pages in this section

- **[Tools](tools/)** — every tool the Studio MCP server exposes to your AI assistant, grouped by feature.

## Where to find the Studio MCP URL

Open your [dashboard](https://web.ankimcp.ai), go to the **Studio** page, and under **Build with your AI** click **Copy Studio MCP URL**.

The URL is `https://studio.ankimcp.ai/mcp`. It's the same for everyone — your account decides what it can see.

## If you're just getting started

These pages assume you've already added Studio to your AI assistant. If you haven't:

- [Anki Studio](/docs/anki-studio/) — what Studio is and the features it gives your AI.
- [Connect MCP clients](/docs/how-to/connect-mcp-clients/) — how to add an MCP server to Claude, ChatGPT and other clients.

---

*Disclaimer: "Anki" is a registered trademark of Ankitects Pty Ltd. AnkiMCP is an independent, community-built project and is **not** affiliated with, endorsed by, or sponsored by Ankitects. MCP is an open standard originated by Anthropic; AnkiMCP is likewise not affiliated with or endorsed by Anthropic.*
