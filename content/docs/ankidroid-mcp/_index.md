---
title: "AnkiMCP for AnkiDroid"
linkTitle: "AnkiMCP for AnkiDroid"
description: "AnkiMCP for AnkiDroid is an Android app that connects your AI to AnkiDroid on your phone, so Claude can read your decks, build cards, and review with you."
keywords:
  - ankidroid ai
  - ankidroid mcp
  - ankidroid claude
  - anki android ai
  - ankimcp android
  - ankidroid flashcards ai
weight: 4
sitemap_priority: 0.8
---

AnkiMCP for AnkiDroid is an Android app that connects your AI assistant to [AnkiDroid](https://github.com/ankidroid/Anki-Android) on your phone. Claude can then read your decks, add and edit notes, and run a review session, using the collection you already study from. You don't need a computer.

{{< callout type="info" >}}
**Early access.** The app is in its first release (0.1.0). It's in testing on Google Play first, then rolls out to everyone.
{{< /callout >}}

## How it works

The app runs next to AnkiDroid and talks to it through AnkiDroid's official API. There are two ways to reach it:

- **Remote access** works with Claude on the web, desktop, or mobile. The app connects your phone to AnkiMCP's tunnel service through its own relay (`ankidroid.ankimcp.ai`), using the same AnkiMCP account as the [Anki add-on](/docs/concepts/add-on-vs-cli/). When Claude needs your phone, a push message wakes the app, and it answers through the tunnel. You need an AnkiMCP account.
- **Local Wi-Fi** works with Claude Desktop or Claude Code on a computer on the same Wi-Fi. The computer talks to your phone directly, and nothing goes through AnkiMCP's servers. You don't need an account.

Your collection stays on your phone. The app sends only the answer to each request your AI makes, and AnkiMCP never stores those answers. See the [Privacy Policy](/privacy/#ankimcp-app-for-android-ankidroid) for details.

## What you need

- **Android 8.0** or later.
- **AnkiDroid 2.24** or later, opened at least once, with its API turned on: **Settings → Advanced → Enable AnkiDroid API**. It's on by default.
- An **AnkiMCP account** for remote access. The tunnel has a [free tier and paid tiers](/pricing/).
- **Google Play services** for automatic wake-ups in remote access. Without them, you can still tap **Connect** yourself.

## Set up remote access

1. Install the app and open it. When it asks for access to AnkiDroid, allow it.
2. On the **Remote** tab, tap **Sign in**. Open the page it shows, check that the code matches, and approve. You can sign in with Google, GitHub, or email and password. On Android 13 and later, allow notifications when asked.
3. Tap **Connect**. A green dot means the phone is connected.
4. In Claude, go to **Settings → Connectors → Add custom connector**. Paste the MCP server URL from the app (tap **Copy URL**), then sign in with the same AnkiMCP account. The URL is the same for everyone:

   ```text
   https://ankidroid.ankimcp.ai/mcp
   ```

5. Ask Claude: **"list my Anki decks"**.

This address is separate from the [Anki add-on's tunnel](/docs/how-to/connect-claude/), so you can connect both your phone and your computer at the same time.

After that, Claude wakes your phone whenever it needs it. The app disconnects when the screen turns off, or after 15, 30, or 60 idle minutes (you choose). The **Remote access** switch at the top of the Remote tab turns remote access off completely.

## Set up local Wi-Fi

1. On the **Local** tab, turn on **Local server (Wi-Fi)**.
2. Turn on **Require access token** if you share the Wi-Fi with people you don't trust. Without it, anyone on the same network can reach your collection.
3. Tap **Copy URL** (and **Copy token** if you turned on **Require access token**), or tap **Share** to send both to your computer.
4. Add the URL to Claude Code or Claude Desktop on that computer, as shown below.

The URL looks like `http://192.168.1.20:8765/mcp`: your phone's Wi-Fi address, the port (8765 unless you change it on the **Local server** card), and `/mcp`. Replace the example address below with yours.

Claude on the web, and Claude Desktop's own **custom connectors**, can't use local mode. They connect from Anthropic's cloud, which can't reach a phone on your home network.

### Claude Code

```bash
claude mcp add --transport http ankidroid http://192.168.1.20:8765/mcp
```

With **Require access token** on, add the token as a header:

```bash
claude mcp add --transport http ankidroid http://192.168.1.20:8765/mcp \
  --header "Authorization: Bearer YOUR_TOKEN"
```

### Claude Desktop

Claude Desktop reaches the phone through [mcp-remote](https://www.npmjs.com/package/mcp-remote), so you need [Node.js](https://nodejs.org/) installed. Open **Settings → Developer → Edit Config**, add this to `claude_desktop_config.json`, and restart Claude Desktop:

```json
{
  "mcpServers": {
    "ankidroid": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "http://192.168.1.20:8765/mcp", "--allow-http", "--transport", "http-only"]
    }
  }
}
```

With **Require access token** on, pass the token through an environment variable:

```json
{
  "mcpServers": {
    "ankidroid": {
      "command": "npx",
      "args": [
        "-y", "mcp-remote", "http://192.168.1.20:8765/mcp", "--allow-http", "--transport", "http-only",
        "--header", "Authorization:${AUTH_HEADER}"
      ],
      "env": { "AUTH_HEADER": "Bearer YOUR_TOKEN" }
    }
  }
}
```

Keep `Authorization:${AUTH_HEADER}` exactly as written, with no space after the colon. The space lives in the `env` value instead, so `npx` doesn't split it.

### If the computer can't reach the phone

- **On a Mac,** allow the app that runs Claude Code or Claude Desktop (Terminal, iTerm, or Claude) under **System Settings → Privacy & Security → Local Network**. Without it, the connection fails with `EHOSTUNREACH`.
- **The phone's address changed.** It changes when the phone joins another network or gets a new address from the router. Update the URL on your computer, or reserve a fixed address for the phone in your router.
- **Guest Wi-Fi** often blocks devices from talking to each other. Put both on the same regular network.
- **The phone stops answering with the screen off.** Nothing can wake the app in local mode, so turn battery optimisation off for AnkiMCP (see [Keep the app awake](#keep-the-app-awake)).
- **After a reboot,** the local server stays off until you open the app.

While the server runs, a **Local MCP server** notification stays up with a **Stop local server** button. The app doesn't need to stay open.

{{< callout type="warning" >}}
Local mode is plain, unencrypted HTTP. Everything crosses your Wi-Fi in the open, including the token. Use it only on a home network you trust.
{{< /callout >}}

## Plans

You don't need a paid plan to use the app. Your AnkiMCP plan covers your whole account, so the phone and the desktop add-on share it:

- **Free:** 100 tool calls a month, shared between your phone and your computer. A tool call is one action your AI takes in Anki, like listing decks or adding a note. The count resets on the 1st of each month (UTC).
- **Plus and Pro:** no request limit.

You can subscribe in the app through Google Play, or on the web. Manage the subscription where you bought it: a Google Play subscription is changed or cancelled in the Play Store, and a web subscription in your [dashboard](https://web.ankimcp.ai). See [pricing](/pricing/) for what each plan includes.

## Keep the app awake

Many Android phones freeze background apps to save battery. This is common on Xiaomi, Redmi, Poco, Realme, Oppo, OnePlus, Vivo, iQOO, Huawei, and Honor. If requests time out, allow **both** AnkiMCP and AnkiDroid to run in the background. On these phones, the **Battery** card in the app shows the exact steps for your phone and has buttons that open both apps' App info pages.

## Limitations

- AnkiDroid's API doesn't support some actions, so the app can't do them. These include unsuspend, unbury, reschedule, creating filtered decks, changing FSRS settings, handling media, and opening AnkiDroid screens.
- Sync isn't automatic. When your AI asks to sync, the app shows a **Tap to sync AnkiDroid** notification. If you also study on other devices, sync first so your AI sees the latest cards.
- Each request can change up to 20 notes or cards. Lookups by ID take up to 100 notes or cards at a time, and card lists come in pages of up to 200.
- There's no iOS version.

## Get help

If something goes wrong, open the **Log** tab, tap **Share log**, and post it on the [community forum](https://forum.ankimcp.ai/). Your email and tokens are removed from the log before you share it.

To delete your AnkiMCP account, see [Delete your account](/delete-account/).

---

*Disclaimer: "Anki" is a registered trademark of Ankitects Pty Ltd. AnkiMCP is an independent, community-built project and is **not** affiliated with, endorsed by, or sponsored by Ankitects or the AnkiDroid project. Android and Google Play are trademarks of Google LLC. MCP is an open standard originated by Anthropic; AnkiMCP is likewise not affiliated with or endorsed by Anthropic.*
