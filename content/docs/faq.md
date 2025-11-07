---
title: "Frequently Asked Questions (FAQ)"
linkTitle: "FAQ"
description: "Common questions and answers about Anki MCP, installation, usage, troubleshooting, and AI integration with Anki flashcards"
keywords: ["anki mcp faq", "anki ai integration questions", "claude anki problems", "chatgpt flashcards help", "anki mcp troubleshooting", "model context protocol anki"]
sitemap_priority: 0.8
weight: 2
---

## General Questions

### What is Anki MCP?

Anki MCP is an open-source bridge that connects AI assistants like Claude, ChatGPT, or Cursor to your Anki flashcard application. It uses the Model Context Protocol (MCP) to enable natural language interaction with your study materials. You can create cards, review them, search your decks, and manage your learning - all through conversation with AI.

### Is Anki MCP free?

Yes! Anki MCP is completely free and open-source under the AGPL-3.0-or-later license. You can use it, modify it, and even contribute to its development on [GitHub](https://github.com/anki-mcp/anki-mcp-desktop).

### Do I need to pay for Claude or ChatGPT to use this?

- **Claude Desktop**: Free tier available with usage limits
- **ChatGPT**: Requires ChatGPT Plus subscription ($20/month) for custom GPT access
- **Cursor/Cline**: Free tier available with limited AI requests
- **Claude.ai (Web)**: Free tier with usage limits

The Anki MCP server itself is always free, but the AI services you connect it to may have their own pricing.

### Is this affiliated with Anki or Ankitects?

No. Anki MCP is an independent community project NOT affiliated with, endorsed by, or sponsored by Ankitects Pty Ltd. Anki® is a registered trademark of Ankitects Pty Ltd. This tool simply connects to Anki through the official AnkiConnect plugin.

### What's the difference between Desktop, MCP Clients, and Web modes?

- **Desktop Mode**: For Claude Desktop app on your computer. One-click installation with MCPB bundle.
- **MCP Clients Mode**: For development tools like Cursor IDE or Cline that support MCP protocol.
- **Web Mode**: For web browsers - use with ChatGPT or Claude.ai by running a local server with optional ngrok tunnel.

Choose based on which AI assistant you primarily use.

## Installation Questions

### How do I install Anki MCP?

The installation depends on your chosen mode:

1. **Claude Desktop**: Download the `.mcpb` file from [releases](https://github.com/anki-mcp/anki-mcp-desktop/releases) and drag it into Claude Desktop settings
2. **MCP Clients**: Run `npx anki-mcp-http --stdio` and configure in your client
3. **Web Mode**: Run `npx anki-mcp-http --ngrok` to start server with public tunnel

See our [installation guides](installation/) for detailed steps.

### Do I need to install AnkiConnect?

Yes! AnkiConnect is required for Anki MCP to communicate with your Anki application. Install it from Anki's add-ons menu using code: `2055492159`

Steps:
1. Open Anki
2. Go to Tools → Add-ons
3. Click "Get Add-ons..."
4. Enter code: `2055492159`
5. Restart Anki

### What versions of Anki are supported?

Anki MCP works with:
- Anki 2.1.50 or newer (recommended)
- Anki 23.10+ (latest versions)
- AnkiMobile and AnkiDroid are NOT directly supported (desktop only)

### Do I need Node.js installed?

- **Claude Desktop (MCPB)**: No, everything is bundled
- **NPX usage**: No, npx downloads what's needed temporarily
- **Global installation**: Yes, Node.js 20+ required
- **Development**: Yes, Node.js 20+ required

### Can I use this on mobile (iPhone/Android)?

Not directly. Anki MCP requires the desktop version of Anki with AnkiConnect plugin. However, you can:
1. Use Anki MCP on your computer to create/manage cards
2. Sync with AnkiWeb
3. Review on mobile using the official Anki apps

## Usage Questions

### How do I create flashcards with AI?

Simply ask your AI assistant naturally:
- "Create a flashcard: Front: What is the capital of France? Back: Paris"
- "Make cards from this text: [paste your notes]"
- "Create 10 Spanish vocabulary cards for beginner level"
- "Turn this Wikipedia article into study cards"

The AI will use Anki MCP to create the cards directly in your chosen deck.

### Can AI review my cards with me?

Yes! Start a review session by saying:
- "Let's review my due cards"
- "Help me study my Spanish deck"
- "Review cards from today"

The AI will present cards, wait for your response, and rate them based on your performance (Again, Hard, Good, Easy).

### How do I search for specific cards?

Ask the AI to search using natural language:
- "Find all my Python programming cards"
- "Show cards tagged with 'important'"
- "Search for cards about World War II"
- "Find cards I added last week"

### Can I use images and audio in my cards?

Yes! Anki MCP supports media files:
- Upload images from URLs or local files
- Add audio files for pronunciation
- Include diagrams and charts
- Media is stored in Anki's media folder

Example: "Create a card with this image: [URL] on the front"

### What's the twenty_rules prompt?

The `twenty_rules` prompt is a special command that makes the AI follow Piotr Wozniak's "Twenty Rules of Formulating Knowledge" - evidence-based principles for creating effective flashcards. Use it by saying: "Use the twenty rules to create cards about [topic]"

## Troubleshooting

### "Connection to Anki failed" error

This usually means:
1. **Anki is not running** - Start Anki first
2. **AnkiConnect not installed** - Install addon code `2055492159`
3. **Wrong port** - AnkiConnect uses port 8765 by default
4. **Firewall blocking** - Allow localhost connections

### "No MCP servers found" in Claude Desktop

1. Check config file location:
   - Mac: `~/Library/Application Support/Claude/claude_desktop_config.json`
   - Windows: `%APPDATA%\Claude\claude_desktop_config.json`
2. Restart Claude Desktop after installing
3. Ensure the .mcpb file was properly installed in Extensions

### Cards aren't syncing to AnkiWeb

Anki MCP creates cards locally. To sync:
1. Create/modify cards with AI
2. In Anki, click "Sync" button or press Y
3. Cards will upload to AnkiWeb
4. Other devices will receive cards on next sync

### "Permission denied" error with npx

On macOS/Linux, you might need to clear npm cache:
```bash
npm cache clean --force
npx anki-mcp-http --stdio
```

### Web mode: "Cannot access from browser"

When using `--ngrok` flag:
1. Ensure ngrok is installed: `npm install -g ngrok`
2. Set up ngrok account and auth token (free at ngrok.com)
3. Use the provided `https://xxx.ngrok-free.app` URL, not localhost
4. Keep the terminal window open while using

### AI creates cards in wrong deck

Specify the deck explicitly:
- "Create this card in my 'Spanish' deck"
- "Add to the 'Medical School' deck"
- Default deck is used if not specified

### Cards have weird formatting or HTML

Anki supports HTML in cards. The AI might add:
- **Bold text**: `<b>important</b>`
- **Italics**: `<i>emphasis</i>`
- **Line breaks**: `<br>`

This is normal. The formatting will display correctly during reviews.

## Security & Privacy

### Is my data safe?

- **Local mode**: All data stays on your computer
- **Web mode with ngrok**: Creates secure tunnel, but URL should be kept private
- Cards are never sent to our servers (we don't have any)
- AI providers (Claude/ChatGPT) process your requests per their privacy policies

### Can others access my Anki through this?

- **Desktop/STDIO modes**: No, completely local
- **HTTP mode (localhost)**: No, local only
- **HTTP mode with ngrok**: Only if someone has your unique ngrok URL

Never share your ngrok URL publicly.

### What data does the AI see?

When you interact with Anki MCP, the AI can:
- Read card contents you search for
- See deck names and structure
- Access cards you're reviewing
- View media file names

The AI only sees what you explicitly ask it to work with.

## Advanced Usage

### Can I customize card templates?

Yes, but through Anki itself. Anki MCP uses your existing note types and templates. Customize them in Anki (Tools → Manage Note Types), and the AI will use your templates when creating cards.

### How do I use with multiple profiles?

Anki MCP connects to whichever Anki profile is currently open. To switch:
1. Close Anki
2. Open Anki with desired profile
3. The AI will now work with that profile

### Can I automate bulk card creation?

Yes! Examples:
- "Create 50 cards from this PDF about biology"
- "Generate cards for all terms in this glossary"
- "Make comprehensive cards from these lecture notes"

The AI will process large requests and create multiple cards efficiently.

### Does it work with filtered decks?

Partial support. Anki MCP can:
- Review cards from filtered decks
- Search within them
- But cannot create cards directly in filtered decks (Anki limitation)

### Can multiple people use my Anki MCP server?

Technically yes with HTTP mode, but:
- Only one person can review at a time
- All changes affect the same Anki profile
- Better to have individual installations

## Getting Help

### Where can I get more help?

- **Documentation**: [ankimcp.ai/docs](https://ankimcp.ai/docs)
- **GitHub Issues**: [Report bugs or request features](https://github.com/anki-mcp/anki-mcp-desktop/issues)
- **Discord**: [Join our community](https://discord.gg/JVNcxNB3e7)
- **Email**: support@ankimcp.ai

### How do I report a bug?

Create an issue on [GitHub](https://github.com/anki-mcp/anki-mcp-desktop/issues) with:
1. Your setup (OS, Anki version, mode used)
2. Steps to reproduce the problem
3. Error messages (if any)
4. What you expected to happen

### Can I contribute to the project?

Absolutely! We welcome:
- Code contributions (pull requests)
- Bug reports and feature requests
- Documentation improvements
- Translations
- Testing and feedback

See our [GitHub repository](https://github.com/anki-mcp/anki-mcp-desktop) to get started.

### Is there a roadmap?

Check our [GitHub project board](https://github.com/anki-mcp/anki-mcp-desktop/projects) for planned features. Currently working towards:
- Version 1.0 stable release
- Better media handling
- Advanced card statistics
- Improved sync features
- Browser extension support

---

*Don't see your question? Ask on [Discord](https://discord.gg/JVNcxNB3e7) or [create an issue](https://github.com/anki-mcp/anki-mcp-desktop/issues)!*