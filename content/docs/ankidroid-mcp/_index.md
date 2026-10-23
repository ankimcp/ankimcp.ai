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

You can use both at the same time, and the phone's remote access works alongside the add-on on your computer.

Your collection stays on your phone. In remote access, only your AI's requests and the app's answers pass through AnkiMCP's relay, and they're never stored. See the [Privacy Policy](/privacy/#ankimcp-app-for-android-ankidroid) for details.

## Get started

- **[Remote access](/docs/ankidroid-mcp/remote-access/)**: sign in, connect, and add one connector in Claude. Works with Claude everywhere.
- **[Local Wi-Fi](/docs/ankidroid-mcp/local-wifi/)**: connect Claude Desktop or Claude Code on your home network, with no account.

## What you need

- **Android 8.0** or later.
- **AnkiDroid 2.24** or later, opened at least once, with its API turned on: **Settings → Advanced → Enable AnkiDroid API**. It's on by default.
- An **AnkiMCP account** for remote access. The tunnel has a [free tier and paid tiers](/pricing/).
- **Google Play services** for automatic wake-ups in remote access. Without them, you can still tap **Connect** yourself.

## Google Play or GitHub

The app is on Google Play, and as an APK on [GitHub Releases](https://github.com/ankimcp/ankidroid-mcp/releases). Both builds run the same code, but they're signed with different keys:

- You can't install one over the other. To switch, uninstall first. You'll need to sign in and set things up again; your AnkiDroid collection isn't touched.
- Google Play updates the app automatically. The GitHub APK you update by hand.
- Plus and Pro are sold through Google Play. Install the app from Google Play to subscribe in the app. A plan bought on the web works in either build.

## Plans

You don't need a paid plan to use the app. Your AnkiMCP plan covers your whole account, so the phone and the desktop add-on share it:

- **Free:** 100 tool calls a month, shared between your phone and your computer. A tool call is one action your AI takes in Anki, like listing decks or adding a note. The count resets on the 1st of each month (UTC).
- **Plus and Pro:** no request limit.

You can subscribe in the app through Google Play, or on the web. Manage the subscription where you bought it: a Google Play subscription is changed or cancelled in the Play Store, and a web subscription in your [dashboard](https://web.ankimcp.ai). See [pricing](/pricing/) for what each plan includes.

## Keep the app awake

Many Android phones pause background apps to save battery. This is common on Xiaomi, Redmi, Poco, Realme, Oppo, OnePlus, Vivo, iQOO, Huawei, and Honor. If requests time out, allow **both** AnkiMCP and AnkiDroid to run in the background. On these phones, the **Battery** card in the app shows the exact steps for your phone and has buttons that open both apps' App info pages.

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
