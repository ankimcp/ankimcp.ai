---
title: "Reference"
description: "Where to look up AnkiMCP tools, settings, and facts: the Anki add-on's tools and configuration, Anki Studio's tools, and the open-source CLI."
weight: 6
---

Need to look up a tool, a setting, or an exact fact? Start here.

## Anki add-on

The add-on is the version that installs inside the Anki desktop app and starts on its own. It's what most people use.

- **[Tools](addon/tools/)** — every MCP tool, resource and prompt the add-on exposes to your AI assistant, with the destructive opt-in ones flagged.
- **[Configuration](addon/configuration/)** — every configuration key, its type, its default, and what it changes.

## Anki Studio

Anki Studio is AnkiMCP's cloud side: features your AI reaches through the Studio MCP endpoint, separate from the add-on.

- **[Tools](studio/tools/)** — every MCP tool the Studio server exposes to your AI assistant, grouped by feature.

## On GitHub

The source of truth lives next to the code:

- **[CLI server](https://github.com/ankimcp/anki-mcp-server)** — tools, settings, and setup details for the command-line server
- **[Anki add-on](https://github.com/ankimcp/anki-mcp-server-addon)** — everything specific to the add-on that runs inside Anki
