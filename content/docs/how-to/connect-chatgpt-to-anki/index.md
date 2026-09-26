---
title: "How to Connect ChatGPT to Anki"
linkTitle: "Connect ChatGPT to Anki"
description: "Connect ChatGPT to Anki with the AnkiMCP add-on's built-in tunnel, so ChatGPT can read your decks and build cards. No Node.js, no extra add-ons."
keywords:
  - chatgpt anki
  - connect chatgpt to anki
  - anki chatgpt
  - chatgpt anki flashcards
  - anki ai remote access
  - anki mcp tunnel
weight: 2
sitemap_priority: 0.8
aliases:
  - /docs/installation/web/
---

**Connect ChatGPT to Anki with the AnkiMCP add-on's built-in tunnel, so ChatGPT can read your decks and build cards from your browser.**

ChatGPT runs in the cloud, so it can't see Anki on your computer. The AnkiMCP **add-on** fixes this. It runs inside Anki and, with one click, gives your collection a secure public web address that ChatGPT can reach. You turn on the tunnel, sign in once, and paste the address into ChatGPT.

## What you need

- A **ChatGPT account** on a plan that lets you create MCP apps under **Plugins**. You'll add the tunnel as one. OpenAI lists which plans include this on its [Developer mode and MCP apps page](https://help.openai.com/en/articles/12584461-developer-mode-and-mcp-apps-in-chatgpt).
- **Anki 25.07 or later**, open on your computer. Get it from [apps.ankiweb.net](https://apps.ankiweb.net/).
- The **AnkiMCP add-on** for Anki, code `124672614`. You'll install it below.
- An **AnkiMCP account**. The tunnel has a [free tier and a paid tier](/pricing/). You sign in the first time you connect it.

**Time:** about 5 minutes.

## Why a tunnel?

ChatGPT runs on a remote server, not on your machine. It has no way to reach `localhost`, where Anki lives. The add-on's tunnel relays messages between ChatGPT and your local Anki over a secure, signed-in connection. Your cards never leave your control, and the link is private to your account.

## Step 1: Install the AnkiMCP add-on

The add-on starts a small server inside Anki. It launches on its own every time you open Anki.

1. Open Anki.
2. Go to **Tools → Add-ons → Get Add-ons...**
3. Enter this code: `124672614`
4. Click **OK**, then restart Anki.

<img src="install-ankimcp-addon.png" width="582" alt="Anki's Install Add-on dialog with the AnkiMCP add-on code 124672614 entered in the Code field." />

## Step 2: Connect the tunnel and sign in

Now turn on the tunnel so your Anki gets a public web address.

1. Go to **Tools → AnkiMCP Server Settings...**
2. Click **Connect Tunnel**.
3. A login dialog shows a one-time code. Click **Open Browser** and enter that code on the page that opens.
4. Approve the sign-in. The add-on saves your login, so you won't repeat this each time.

<img src="ankimcp-login-code.png" width="427" alt="Login to AnkiMCP dialog showing a one-time code, an Open Browser button, and a waiting-for-authorization status." />

## Step 3: Copy the tunnel URL

The tunnel address is the same for everyone:

```text
https://tunnel.ankimcp.ai/mcp
```

It's safe to share, because it only works after you sign in — requests reach your Anki only when the AI app is signed in with **your** account. Copy that URL. You'll paste it into ChatGPT next.

<img src="tunnel-connected.png" width="449" alt="AnkiMCP Server Settings with the Cloud Tunnel connected, showing the signed-in account and the permanent tunnel URL https://tunnel.ankimcp.ai/mcp with a Copy button." />

## Step 4: Add the tunnel to ChatGPT

Open [chatgpt.com](https://chatgpt.com) in your browser and add the tunnel as an MCP app.

1. In the left sidebar, click **Plugins**.

<img src="chatgpt-sidebar-plugins.png" width="740" alt="ChatGPT's left sidebar with New chat, Scheduled, Library, Plugins, and Explore. Plugins is the fourth item." />

2. On the **Plugins** page, click **Add** in the top-right corner, then choose **Create MCP App**.

<img src="chatgpt-add-create-mcp-app.png" width="740" alt="ChatGPT's Plugins page with the Add menu open in the top-right corner, showing Create plugin, Upload plugin archive, and Create MCP App." />

3. The **Create MCP App** dialog opens. Fill it in:
   - **Name**: something like `AnkiMCP.ai`. The icon and description are optional.
   - **Connection**: keep **Server URL** selected and paste your tunnel URL. Ignore the **Tunnel** option — that's ChatGPT's own feature, not the AnkiMCP tunnel.
   - **Authentication**: leave it on **OAuth**. Don't open **Advanced OAuth settings**; ChatGPT reads the right settings from the URL.
   - Check **I understand and want to continue** to accept ChatGPT's custom-MCP risk notice, then click **Create**.

<img src="chatgpt-create-mcp-app.png" width="609" alt="ChatGPT's Create MCP App dialog with an Elevated risk badge: Name and Description fields, Connection set to Server URL, Authentication set to OAuth, an Advanced OAuth settings row, the I understand and want to continue checkbox, and Cancel and Create buttons." />

4. ChatGPT shows a **Connect AnkiMCP.ai** screen that explains permissions. Click **Continue to AnkiMCP.ai**.

<img src="chatgpt-connect-ankimcp.png" width="492" alt="ChatGPT's Connect AnkiMCP.ai dialog listing Permissions always respected, You're in control, and Connectors may introduce risk, with a Continue to AnkiMCP.ai button." />

5. AnkiMCP opens and asks you to **Grant Access to ChatGPT**. Sign in if prompted, then click **Yes**.

<img src="ankimcp-grant-access-chatgpt.png" width="565" alt="AnkiMCP's Grant Access to ChatGPT page listing Offline Access, Access your Anki via the AnkiMCP tunnel (MCP), Email address, User roles, and User profile, with Yes and No buttons." />

6. Back in ChatGPT, AnkiMCP.ai now shows under **Installed** on the Plugins page. Click it to open its details, where a **Try in chat** button starts a conversation with the plugin ready to use.

<img src="chatgpt-plugins-installed.png" width="430" alt="ChatGPT's Plugins page with AnkiMCP.ai shown under Installed." />

<img src="chatgpt-plugin-try-in-chat.png" width="740" alt="The AnkiMCP.ai plugin details page in ChatGPT, showing one app named AnkiMCP.ai and a Try in chat button." />

## Check it worked

Keep Anki open, then start a chat and type `@`, pick **AnkiMCP.ai** from the list, and ask: **"fetch anki decks"**.

If it names your real decks and card counts, the tunnel works. You can now ask it to make cards, search your collection, or review with you. Mentioning the plugin with `@` tells ChatGPT to use it for that message; after the first time, it usually picks AnkiMCP.ai on its own whenever you talk about Anki.

<img src="chatgpt-fetch-anki-decks.png" width="682" alt="A ChatGPT conversation: the user message @AnkiMCP.ai fetch anki decks, and ChatGPT replying that it can access the Anki collection through AnkiMCP.ai and listing 42 decks with 34,589 cards." />

## Fix common problems

**ChatGPT can't connect.**
Make sure Anki is open and the tunnel shows as connected in **Tools → AnkiMCP Server Settings...**. The tunnel only relays while Anki is running. Reconnect the tunnel if needed.

**ChatGPT connects but sees no decks.**
Anki itself may be closed. Open Anki and confirm the tunnel is connected in **Tools → AnkiMCP Server Settings...**.

**Sign-in didn't open my browser.**
The login dialog shows a backup link and code. Open the link and enter the code to approve.

## Common questions

**Do I have to pay?**
The add-on is free. The tunnel has a free tier to get started and a paid tier for higher limits — see [pricing](/pricing/).

## Next steps

- New to local vs. remote? Read [Remote vs local access](/docs/concepts/remote-vs-local/) to choose the right path.
- Want better cards? Try these [AI prompts for Anki](/docs/how-to/anki-ai-prompts/).

---

*Disclaimer: "Anki" is a registered trademark of Ankitects Pty Ltd. AnkiMCP is an independent, community-built project and is **not** affiliated with, endorsed by, or sponsored by Ankitects. MCP is an open standard originated by Anthropic; AnkiMCP is likewise not affiliated with or endorsed by Anthropic.*
