---
title: "Connect ChatGPT & Claude.ai to Anki - Web Mode Setup"
linkTitle: "Web Installation"
description: "Step-by-step guide to connect web-based AI assistants like ChatGPT, Claude.ai, and Gemini to your Anki flashcards using integrated ngrok tunneling."
keywords: ["chatgpt anki", "claude.ai anki", "anki web mode", "ai flashcards online", "ngrok anki", "gemini anki"]
weight: 2
sitemap_priority: 0.9
---

This guide is for **web-based AI assistants** like ChatGPT, Claude.ai, Gemini, or any AI that works in a browser. If you use Claude Desktop, see the [Desktop Installation Guide](../desktop) instead.

## How It Works

You'll run a small server on your computer. Your AI assistant connects to it over the internet. Think of it like opening a door for your AI to talk to Anki.

```
Your Computer                    The Internet               AI Assistant
┌──────────────┐                                           ┌────────────┐
│ Anki Desktop │ ←→ ankimcp server ←→ ngrok tunnel ←→      │ ChatGPT    │
└──────────────┘                                           │ Claude.ai  │
                                                           └────────────┘
```

## What You Need

1. **Anki Desktop** - Your flashcard app
   Download: [apps.ankiweb.net](https://apps.ankiweb.net/)

2. **AnkiConnect Plugin** - Lets other apps talk to Anki
   Download: [ankiweb.net/shared/info/2055492159](https://ankiweb.net/shared/info/2055492159)

3. **Node.js** - To run the server
   Download: [nodejs.org](https://nodejs.org/) (version 20 or newer)

4. **ngrok** (for tunneling) - Creates a secure tunnel to your computer
   - Download: [ngrok.com](https://ngrok.com)
   - Install: `npm install -g ngrok`
   - Get auth token from [dashboard.ngrok.com](https://dashboard.ngrok.com)
   - Setup: `ngrok config add-authtoken <your-token>`

## Installation Steps

### Method 1: One Command (Recommended - v0.8.0+)

**New in v0.8.0:** Start the server with integrated ngrok tunneling using just one command!

**Option A: Quick Start (No Installation)**

Open your terminal and run:

```bash
npx anki-mcp-http --ngrok
```

**Option B: Install Globally (Shorter Command)**

If you plan to use this often, install it once:

```bash
npm install -g anki-mcp-http
```

Then you can run it with the shorter command:

```bash
anki-mcp-http --ngrok
```

**Either way**, you'll see:
```
╔════════════════════════════════════════════════════════════════╗
║              AnkiMCP HTTP Server v0.8.0                        ║
╚════════════════════════════════════════════════════════════════╝

🚀 Server running on: http://127.0.0.1:3000
🔌 AnkiConnect URL:   http://localhost:8765
🌐 Ngrok tunnel:      https://abc123.ngrok-free.app

Share this URL with your AI assistant:
  https://abc123.ngrok-free.app
```

Copy the ngrok URL (the `https://abc123.ngrok-free.app` part) - you'll need it in the next step.

**Leave this terminal window open** - the server needs to stay running.

**Benefits:**
- ✅ One command instead of two
- ✅ Automatic cleanup when you press Ctrl+C
- ✅ URL displayed clearly in the banner
- ✅ Works with custom ports: `anki-mcp-http --port 8080 --ngrok`

### Method 2: Manual Setup (Alternative)

If you prefer to manage ngrok separately, you can still use the manual method:

**Step 1:** Start the server in one terminal:

```bash
npx anki-mcp-http
```

You'll see:
```
🚀 Server running on: http://127.0.0.1:3000
🔌 AnkiConnect URL: http://localhost:8765
```

**Step 2:** Open a **second** terminal and start ngrok:

```bash
ngrok http 3000
```

You'll see:
```
Forwarding  https://abc123.ngrok-free.app → http://localhost:3000
```

Copy the URL (the `https://abc123.ngrok-free.app` part).

**Keep both terminal windows open.**

## Connect Your AI

Now connect your AI assistant to the server using the ngrok URL you copied.

**For Claude.ai:**

In Claude's web interface, go to Settings → Connectors → Add custom connector, then paste your ngrok URL.

Full tutorial: [Getting Started with Custom Connectors](https://support.claude.com/en/articles/11175166-getting-started-with-custom-connectors-using-remote-mcp)

**For ChatGPT and other AI assistants:**

Check your AI provider's documentation to see if they support custom MCP servers or external tool integration, and follow their connection instructions.

## Try It Out

Once connected, ask your AI:

**"Show me my Anki decks"**

If it works, you'll see your decks! 🎉

## What Your AI Can Do

Once connected, your AI can:

- Show your decks and their stats
- Review cards with you
- Create new flashcards
- Search your cards
- Update existing cards
- Help explain concepts

## Server Options

You can customize the server:

```bash
# Start with ngrok tunnel (v0.8.0+)
npx anki-mcp-http --ngrok

# Use a different port
npx anki-mcp-http --port 8080

# Different port + ngrok
npx anki-mcp-http --port 8080 --ngrok

# Allow connections from other computers on your network
npx anki-mcp-http --host 0.0.0.0

# Connect to AnkiConnect on another computer
npx anki-mcp-http --anki-connect http://192.168.1.100:8765

# Combine all options
npx anki-mcp-http --port 8080 --anki-connect http://localhost:8765 --ngrok
```

## Troubleshooting

**AI says it can't connect:**
- If using `--ngrok`: Make sure the terminal window is still open
- If using manual method: Make sure both terminal windows are still open (server + ngrok)
- Check that Anki Desktop is running
- Try the ngrok URL in your browser - you should see a response

**Server won't start:**
- Make sure Node.js is installed: `node --version`
- Should show v20 or higher

**ngrok fails with --ngrok flag:**
- Make sure ngrok is installed: `npm install -g ngrok`
- Make sure you've configured your auth token: `ngrok config add-authtoken <your-token>`
- Get your token from [dashboard.ngrok.com](https://dashboard.ngrok.com)
- If ngrok fails, the server will still start in local mode (you can use manual method)

**ngrok tunnel closes:**
- ngrok free accounts have time limits
- Just restart the server (with `--ngrok`) or ngrok manually
- Your AI will need the new URL

**Still not working?**
See [Getting Help](../getting-help) for support options.

## Security Note

The ngrok URL is public (anyone with the link can access it). Only share it with trusted AI assistants. When you're done studying:

- **With `--ngrok`:** Press Ctrl+C to stop both the server and tunnel
- **With manual method:** Close both terminal windows to stop the server and tunnel

## Next Steps

- Try asking your AI to review a deck with you
- Have it create flashcards from articles or notes
- Ask it to explain difficult concepts on your cards

Happy studying! 📚
