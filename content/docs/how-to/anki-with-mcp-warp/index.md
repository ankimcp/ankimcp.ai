---
title: "Use AnkiMCP with MCP Warp: One Tunnel for Anki and Every Other MCP Server"
linkTitle: "Use with MCP Warp"
description: "Already running MCP Warp for other MCP servers? Add AnkiMCP to the same tunnel and reach Anki from claude.ai, the Claude mobile apps, ChatGPT, or Claude Code. Covers the add-on (HTTP) and the CLI (STDIO)."
keywords:
  - anki mcp warp
  - mcp warp anki
  - anki mcp tunnel
  - expose anki mcp server
  - anki claude mobile
  - anki mcp stdio http
weight: 11
sitemap_priority: 0.7
---

**AnkiMCP ships its own managed tunnel, and for most people that's the right way to reach Anki from a web or mobile AI. But if you already run [MCP Warp](https://mcpwarp.io) to expose other MCP servers, you don't need a second tunnel: add AnkiMCP to your MCP Warp config and the same `mcpwarp up` covers Anki too.**

MCP Warp is a separate product by the same author as AnkiMCP. It works like ngrok, but built for MCP: every local MCP server you list gets its own public address, protected by OAuth sign-in, so there is no anonymous access. Unlike the AnkiMCP tunnel, it isn't tied to one server — Anki sits next to your notes server, your database server, or whatever else you've plugged in.

## Which tunnel should you use?

| | AnkiMCP tunnel | MCP Warp |
|---|---|---|
| **Built for** | Anki only | Any MCP server |
| **Setup** | Sign in from the add-on or CLI | CLI + a config file |
| **Sign-in** | Your ankimcp.ai account | Your MCP Warp account (OAuth) |
| **Good fit when** | Anki is the only thing you expose | You already expose other servers |
| **Pricing** | [Free and paid tiers](/pricing/) | [Free 1 server / 100 requests a month, Plus $5, Pro $10](https://mcpwarp.io/pricing/) |

If Anki is the only MCP server you care about, stick with the [managed tunnel](/docs/concepts/remote-vs-local/) — it needs no config file and no extra CLI. The rest of this page is for people who run MCP Warp anyway.

## What you need

- **Anki open** on the computer that runs MCP Warp. Both tunnels only relay to a running Anki; neither is a cloud copy of your cards.
- The **MCP Warp CLI** installed and signed in. Follow [Get started](https://mcpwarp.io/docs/get-started/): install, run `mcpwarp login`, and pick a username at [web.mcpwarp.io](https://web.mcpwarp.io) — the CLI refuses to start a tunnel without one (`USERNAME_REQUIRED`).
- One of the two AnkiMCP servers, below. Not sure which you have? See [Add-on vs CLI](/docs/concepts/add-on-vs-cli/).

**Time:** about 5 minutes if MCP Warp is already set up.

## Step 1: Add AnkiMCP to your MCP Warp config

MCP Warp reads `~/.mcpwarp/config.json`. It can expose two kinds of server, and AnkiMCP comes in both shapes.

{{< tabs >}}

{{< tab name="Add-on (HTTP)" selected=true >}}

The [AnkiMCP add-on](/docs/how-to/connect-mcp-clients/) runs a Streamable HTTP server inside Anki at `http://127.0.0.1:3141/`. Point MCP Warp at that address as an `http` server:

```json
{
  "servers": [
    {
      "name": "anki",
      "kind": "http",
      "url": "http://127.0.0.1:3141/"
    }
  ]
}
```

If the file already lists other servers, add only the `anki` entry to the `servers` array.

Keep the `url` on `127.0.0.1`. MCP Warp forwards requests to the add-on under that local address, so the add-on's [DNS-rebinding protection](/docs/concepts/remote-access-security/) passes as-is — no `http_allowed_hosts` change, no restart.

{{< /tab >}}

{{< tab name="CLI (STDIO)" >}}

The [AnkiMCP CLI](/docs/how-to/connect-mcp-clients/) runs as a subprocess and talks to Anki through the AnkiConnect add-on. MCP Warp starts it for you and bridges STDIO to Streamable HTTP, so there's no local port involved at all. You need Node.js 22.12 or newer and [AnkiConnect](https://ankiweb.net/shared/info/2055492159) installed in Anki.

```json
{
  "servers": [
    {
      "name": "anki",
      "kind": "stdio",
      "command": "npx",
      "args": ["-y", "@ankimcp/anki-mcp-server", "--stdio"],
      "env": { "ANKI_CONNECT_URL": "http://localhost:8765" }
    }
  ]
}
```

If you installed the CLI globally (`npm install -g @ankimcp/anki-mcp-server`), use `"command": "ankimcp"` with `"args": ["--stdio"]` instead. On Windows, `npx` is a `.cmd` shim; MCP Warp's [STDIO guide](https://mcpwarp.io/docs/how-to/expose-a-stdio-server/) explains how to point at the underlying script via `node`.

{{< /tab >}}

{{< /tabs >}}

The `name` becomes part of your public address, so keep it short and lowercase (`anki` works).

## Step 2: Start the tunnel

```bash
mcpwarp status   # validates the config
mcpwarp up
```

`mcpwarp up` prints one public URL per server. Yours looks like:

```
https://anki-yourname.tunnel.mcpwarp.io/mcp
```

Keep that terminal open, and keep Anki open. Close either one and the AI loses its way to your cards.

## Step 3: Connect your AI

Any client that speaks Streamable HTTP can use the URL. The ones people ask about:

**claude.ai and the Claude mobile apps.** Add a custom connector on the web: enter a name and your `*.tunnel.mcpwarp.io/mcp` URL, click **Continue**, keep **Sign in now** and **Register automatically** selected, click **Add**, and finish the OAuth sign-in. Connectors you add on claude.ai show up in the Claude iOS and Android apps the next time you sign in there — so you set it up once on the web and review from your phone. Full steps: [Connect Claude](https://mcpwarp.io/docs/how-to/connect-claude/) on the MCP Warp docs.

**ChatGPT.** Add the same URL as a connector, exactly as in [Connect ChatGPT to Anki](/docs/how-to/connect-chatgpt-to-anki/), substituting the MCP Warp address for the AnkiMCP tunnel address.

**Claude Code.**

```bash
claude mcp add --transport http anki https://anki-yourname.tunnel.mcpwarp.io/mcp
claude mcp login anki
```

## Check it worked

With Anki open and `mcpwarp up` running, ask your assistant: **"List my Anki decks."** If it names your decks, the whole chain works.

## Fix common problems

**`USERNAME_REQUIRED` when running `mcpwarp up`.**
Sign in at [web.mcpwarp.io](https://web.mcpwarp.io) and choose a username first. The username is part of every public URL, so the CLI can't start without it.

**The assistant connects but sees no tools, or times out.**
Check that Anki is open. For the add-on, open [http://127.0.0.1:3141/](http://127.0.0.1:3141/) in your browser. For the CLI, open [http://localhost:8765](http://localhost:8765) — you should see `AnkiConnect`.

**The server keeps restarting (CLI).**
MCP Warp gives up after 10 crashes in a row without a 60-second healthy run. Run the command from your config by hand in a terminal to see the actual error — usually Node.js is too old or AnkiConnect isn't installed.

## Common questions

**Is this instead of the AnkiMCP tunnel?**
It's an alternative, not a replacement. The AnkiMCP tunnel stays the simplest path when Anki is all you expose. MCP Warp earns its place when it's already carrying your other MCP servers.

**Is it safe?**
Every MCP Warp address requires OAuth sign-in, so nobody reaches your Anki without your account. The add-on keeps its [DNS-rebinding protection](/docs/concepts/remote-access-security/) on, because MCP Warp talks to it over the local address; you don't open any port or allow-list any hostname.

**Does my collection go through MCP Warp's servers?**
Requests and responses pass through the tunnel in real time, the same way they do with the AnkiMCP tunnel. Your collection stays in your Anki. See [MCP Warp's docs](https://mcpwarp.io/docs/) for its data handling.

**Will there be a tighter Anki integration in MCP Warp?**
Nothing to announce. Today AnkiMCP is just another server in your config, which is the point.

## Next steps

- New to MCP Warp? Start with [Get started](https://mcpwarp.io/docs/get-started/) and [Expose a STDIO server](https://mcpwarp.io/docs/how-to/expose-a-stdio-server/).
- Why a STDIO server needs a bridge to become a web address at all: [From STDIO MCP server to HTTP](https://mcpwarp.io/blog/stdio-mcp-server-to-http/).
- Want Anki reachable without keeping your laptop on? That's [Hosted Anki](/docs/hosted-anki/), which no tunnel can give you.
- Prompts for reviewing and making cards once you're connected: [Anki AI prompts](/docs/how-to/anki-ai-prompts/).

---

*Disclaimer: "Anki" is a registered trademark of Ankitects Pty Ltd. AnkiMCP is an independent, community-built project and is **not** affiliated with, endorsed by, or sponsored by Ankitects. MCP is an open standard originated by Anthropic; AnkiMCP and MCP Warp are likewise not affiliated with or endorsed by Anthropic.*
