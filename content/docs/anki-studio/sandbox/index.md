---
title: "The Sandbox: Build Cards Together With Your AI"
linkTitle: "Sandbox"
description: "A shared workbench where you and your AI draft Anki cards side by side — the AI writes, you polish live in the dashboard, and only approved cards get pushed to your real deck."
keywords:
  - anki card sandbox
  - AI anki cards
  - anki card preview
  - anki card template editor
  - ankimcp sandbox
  - co-edit anki cards
  - anki card images and audio
weight: 3
sitemap_priority: 0.7
draft: false
---

**The sandbox is where cards are made — together.** Your AI drafts a card, you see it render instantly in the dashboard the way Anki will show it, you fix a word or restyle it, and the AI picks up your changes and continues. Nothing touches your real deck until you say so.

{{< zoom-image src="sandbox-overview.png" alt="The Sandbox in Anki Studio: on the left, a live preview of a rendered card comparing Cactus vs Succulent with icons, fact lists and a one-line summary; on the right, the HTML / CSS / JS / Template editor tabs with the card's fields — Question, LeftIcon, LeftName, LeftFacts — and on top, the card chips for the session with Add card and Clear sandbox buttons." width="740" caption="A card rendered live next to its fields and templates — click to enlarge" >}}

## The idea in one paragraph

Making good Anki cards with an AI has an awkward gap: the AI writes HTML it can't see, and you see cards you didn't write. The sandbox closes the gap with one shared, live workspace. You and your AI are editing the same draft at the same time — the AI works through its Studio tools, you work in the dashboard, and every change shows up on the other side almost at once. The preview isn't an imitation: it renders your note type's real styling, template, and scripts the same way Anki does.

## What's in a sandbox

You get one sandbox per account, and it holds **one note type at a time**:

- **The template** — the note type's styling (CSS), scripts (JS), field names, and card layout, usually fetched by your AI straight from your Anki.
- **Draft cards** — each card is just its field values; all cards share the one template.

The editor panel on the right has four tabs: **HTML** (the fields of the card you've selected), **CSS** (the shared stylesheet), **JS** (the shared script), and **Template** (the question and answer layout). The **Show answer / Show question** button flips the preview between the two sides.

Next to it is a small **Refresh preview** button (the circular arrow). Pictures and sounds from your Media Library load through links that expire after 15 minutes, and the preview doesn't renew them on its own. If an image or a sound stops loading after a while, click it and every link is renewed.

{{< zoom-image src="sandbox-refresh-preview.png" alt="The Sandbox editor panel: at the top right, the round-arrow Refresh preview button next to Show answer; below, one card chip, the Add card and Clear sandbox buttons, and the HTML tab showing the card's Front field with a physics question and its Back field with the answer in MathJax followed by an <img src= reference to a Media Library image." width="520" caption="Refresh preview sits next to Show answer; the Back field ends with an image reference from the Media Library — click to enlarge" >}}

You can start from nothing, too: the editors are always there, and typing into them creates a fresh sandbox on the spot — no AI required.

## How many cards you can draft

A sandbox holds up to **20 draft cards** at once. On the **free plan** the dashboard keeps you to **one card per sandbox**; a paid plan lets you stack more, up to that limit of 20. Your AI can add cards up to the same cap.

## Drafts, not storage

The sandbox is a workbench, not a deck. When a card is ready, your AI pushes it to your real Anki over the connection it already has, then removes it from the sandbox. Drafts you leave untouched expire on their own after about **two weeks**. And **Clear sandbox** wipes the whole thing — template, styles, scripts, and every draft — when you want a clean bench.

<img src="sandbox-clear-dialog.png" width="420" alt="The Clear sandbox confirmation dialog: 'This deletes the template, styles, scripts and all draft cards', with Cancel and Clear it buttons." />

## Approving a card into your deck

The sandbox deliberately has **no button that pushes to Anki** — that keeps it a safe draft space. Instead, once you're happy with a card, your AI adds it to your real deck using the very same Anki connection it uses everywhere else (the same tool it would use to add any note), then clears it from the sandbox. So the flow is: **AI drafts → you polish live → you approve → AI pushes to Anki.** Because the push goes through your normal connection, the card lands in whatever deck you tell it, exactly like any other card your AI makes. The one exception: cards that use Media Library files are always pushed with the sandbox's own push tool, which copies the files into Anki first — see [below](#pictures-and-sounds-from-your-media-library).

## Pictures and sounds from your Media Library

A sandbox card can show an image or play a sound straight from your [Media Library](/docs/anki-studio/media-library/). Just ask:

> Put the diagram I captured on page 12 on the front of this card.

> Add the `hola.mp3` clip from my library to the back of each card.

Your AI opens the file in your library and writes a short reference to it into a card field:

- an image: `<img src="ankimcp-media:<id>">`
- a sound: `[sound:ankimcp-media:<id>]`

The `<id>` is the file's ID from your library. These references go in the card's **fields** (the HTML tab), not in the template or the CSS. Unlike a temporary link, they don't expire, so the card keeps working as long as the file is in your library.

**Only images and audio work this way.** PDFs and subtitle files from your library can't go on a card — they're turned away before anything is pushed.

**Cards with library media are pushed with `sandbox_push_card`.** When you approve such a card, your AI uses this sandbox tool instead of adding the note by hand. It copies each picture and sound into your Anki media folder, swaps every reference for the copied file's name, and then adds the note. The result is an ordinary Anki card that works offline and syncs like any other. This works the same with [Hosted Anki](/docs/hosted-anki/).

If a file can't be read or copied, **no card is added** and your AI tells you why. Files that were already copied stay in your Anki media folder and are reused the next time it tries.

**If you delete a file a card still uses**, nothing stops you. The preview then shows a broken image, and pushing that card fails with a "not found" error. Re-upload the file and have your AI point the card at the new one, or drop it from the card.

## What the preview supports today

The preview aims to render cards exactly as Anki does, but not every Anki template feature is built yet. What gets added next from this list is driven by what people ask for.

| Anki feature | Sandbox today |
|---|---|
| `{{Field}}` substitution | ✅ |
| `{{FrontSide}}` on the answer side | ✅ |
| Question / answer side preview | ✅ |
| Note type CSS | ✅ |
| Template `<script>` JS (hints, toggles) | ✅ |
| Shared session JS | ✅ |
| MathJax math (`\(…\)`, `\[…\]`, `<anki-mathjax>`) | ✅ |
| Images by URL (media library) | ✅ |
| Media Library references (`ankimcp-media:…`) | ✅ images and audio |
| Audio `[sound:…]` | ⚠️ plays for URL and `ankimcp-media:` references only |
| Images by bare Anki filename | ❌ |
| Conditional sections `{{#Field}}` / `{{^Field}}` / `{{/Field}}` | ❌ |
| Field filters (`{{hint:…}}`, `{{text:…}}`, `{{furigana:…}}`, …) | ❌ |
| Cloze deletions `{{c1::…}}` | ❌ |
| Special fields (`{{Tags}}`, `{{Deck}}`, `{{Type}}`, `{{Card}}`) | ❌ |
| Type-in answers (`{{type:Field}}`) | ❌ |
| Multiple card templates per note type (e.g. Basic + reversed) | ❌ one template per sandbox |
| Full LaTeX (`[latex]…[/latex]`, `[$]…[$]`, packages, TikZ) | ❌ |
| Night mode preview | ❌ |
| Text-to-speech (`{{tts …}}`) | ❌ |
| Image occlusion | ❌ |

A note on the two conditional rows: the preview doesn't *evaluate* conditionals or filters — it strips the markers and shows the plain field value — so a card that leans heavily on them will look right in real Anki but plainer here. Images and audio show up when they're referenced by a web link or by an `ankimcp-media:` reference to your [Media Library](/docs/anki-studio/media-library/) (see [above](#pictures-and-sounds-from-your-media-library)); a bare Anki filename won't resolve in the preview.

## Common questions

**The image in my preview stopped loading. What happened?**
The preview's links to your Media Library expire after 15 minutes. Click **Refresh preview** next to **Show answer** and they're renewed. The same goes for a sound that won't play. Your card itself is fine — the reference in its field never expires.

## What you need

- **An AnkiMCP account** with the Studio MCP endpoint added to your AI. New to that? See [Connect MCP clients](/docs/how-to/connect-mcp-clients/).
- **Your Anki connected** so the AI can fetch your note type's styling and, later, push the approved cards. Either connection works — see [Add-on vs CLI](/docs/concepts/add-on-vs-cli/).

---

*Disclaimer: "Anki" is a registered trademark of Ankitects Pty Ltd. AnkiMCP is an independent, community-built project and is **not** affiliated with, endorsed by, or sponsored by Ankitects. MCP is an open standard originated by Anthropic; AnkiMCP is likewise not affiliated with or endorsed by Anthropic.*
