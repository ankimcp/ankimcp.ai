---
title: "Authless Access Ends on November 1"
date: 2026-09-26
author: "Anatoly"
author_link: "https://anatoly.dev"
description: "On November 1, 2026 AnkiMCP.ai removes the authless (no-sign-in) tunnel option. All connections will use the standard authenticated OAuth flow. Here's why and what to do."
keywords: ["ankimcp authless", "ankimcp oauth", "ankimcp tunnel authentication", "ankimcp connection change"]
sitemap_priority: 0.6
---

On **November 1, 2026** I'm removing the **Authless access** option from AnkiMCP.ai. After that date, every connection to your tunnel goes through the standard authenticated (OAuth) flow — the one Claude and ChatGPT already use when you sign in with your account.

## Why

**Almost nobody uses it.** Authless mode was added early on, when many MCP clients couldn't handle OAuth. That's no longer the case: Claude, ChatGPT, Cursor, and most other clients now support it out of the box. Today, fewer than **1%** of users connect without authentication.

**It's a security trade-off that no longer pays off.** An authless endpoint is protected only by its URL, and URLs end up in config files, screenshots, and logs. If it leaks, anyone can read and modify your Anki collection until you notice and regenerate it. An authenticated connection is tied to your account and can be revoked at any time from your Tunnel Dashboard. With so few people relying on authless mode, keeping the weaker option around isn't worth it.

**It's blocking the connector directories.** I want AnkiMCP to be listed in the Claude connector directory and the ChatGPT apps directory, so you can add it in a couple of clicks instead of pasting URLs. Those listings require a single, standard authenticated connection flow. A second, unauthenticated path to the same data is a non-starter for a review.

**It's dead code.** AnkiMCP.ai is a one-person project. Every extra code path is something to test, document, and keep secure — I'd rather spend that time on features you actually use.

## What you need to do

**If you connect with your account** — which is almost everyone — nothing changes. You don't need to do anything.

**If you use an authless URL**, switch to the authenticated connection before November 1. It takes a couple of minutes:

- [Connect Claude](/docs/how-to/connect-claude/)
- [Connect ChatGPT](/docs/how-to/connect-chatgpt-to-anki/)
- [Connect Cursor, Cline & other MCP clients](/docs/how-to/connect-mcp-clients/)

Your decks, cards, and settings are not affected. Only the way your AI client connects changes.

On November 1 the **Authless access** toggle disappears from the Tunnel Dashboard, existing authless URLs stop working, and the free tier's separate authless request allowance goes with them.

## If your client doesn't support OAuth

Write to me at [support@ankimcp.ai](mailto:support@ankimcp.ai) or post on the [community forum](https://forum.ankimcp.ai/) before November 1 and tell me which client you use. If there's a real need, I will try to find a solution.

Anatoly
