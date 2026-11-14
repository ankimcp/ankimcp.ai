---
title: "Anki Studio Tool Reference: Every MCP Tool Your AI Can Call"
linkTitle: "Tools"
description: "All 45 MCP tools the Anki Studio server gives your AI, grouped by feature: knowledge maps, Media Library, sandbox, text to speech, PDF Reader and Video Player."
keywords:
  - Anki Studio MCP tools
  - AnkiMCP Studio tool reference
  - Studio MCP tools list
  - pdf_reader tools
  - video_reader tools
  - sandbox tools
  - knowledge map tools
weight: 1
sitemap_priority: 0.7
---

**This page lists everything the Anki Studio MCP server offers your AI assistant: every tool it can call, grouped by feature.** You don't need to memorise any of it — your assistant discovers these automatically. This page is here for when you want to check exactly what exists.

{{< callout type="info" >}}
**This documents Anki Studio**, AnkiMCP's cloud side. The tools that work with the Anki on your computer — through the [AnkiMCP add-on](/docs/reference/addon/tools/) or the CLI — are separate lists, and nothing on this page describes them. See [Add-on vs CLI](/docs/concepts/add-on-vs-cli/) if you're unsure which you have.
{{< /callout >}}

## At a glance

| | Count |
|---|---|
| Tools | **45** |
| ...connection check | 1 |
| ...knowledge maps | 19 |
| ...Media Library | 3 |
| ...sandbox | 10 |
| ...text to speech | 3 |
| ...PDF Reader | 4 |
| ...Video Player | 5 |
| Resources | **0** |
| Prompts | **0** |

Documented against Studio **0.10.2**. The server introduces itself to your AI client as `ankimcp-studio`, version `0.10.2`, at `https://studio.ankimcp.ai/mcp`. Every tool is always available — there are no hidden or opt-in tools. Your account decides what the tools can see; it's never a parameter.

## What's new in 0.10.2

- **9 new tools** for reading what you have open: four `pdf_reader_*` tools for the [PDF Reader](#pdf-reader) and five `video_reader_*` tools for the [Video Player](#video-player).
- **`sandbox_push_card` now copies media into Anki.** Pictures and sounds from your Media Library that a card refers to are copied into Anki's media folder before the note is added. Details are [under the tool](#sandbox).
- **Updated descriptions** on `sandbox_upsert_card`, `sandbox_patch_card`, `sandbox_get_cards`, `media_library_read_file` and `media_library_read_directory`. They now tell your AI how to refer to Media Library files in a card, and that the library can hold PDFs and subtitle files. Their parameters didn't change.

Nothing was renamed or removed.

{{< callout type="warning" >}}
**To see the new tools, remove the Studio connector in Claude or ChatGPT and add it again.** Your existing connection keeps working, but it won't list the new tools until you do. See [Keeping the tool list fresh](#keeping-the-tool-list-fresh).
{{< /callout >}}

## Connection check

One tool to check that your AI is connected.

- **`ping`** — Health check. Optional `message`, which it echoes back. Returns the echo and your user ID. Changes nothing.

## Knowledge maps

Build and edit your learning roadmaps. See [Knowledge Roadmap](/docs/anki-studio/knowledge-roadmap/).

Limits that apply across these tools: a map or folder `title` is 1–200 characters, a node `label` up to 200, a `description` up to 2,000, and a node's `data` up to 8,192 characters. The only map type today is `"roadmap"`. **Free plan: 1 knowledge map.**

- **`knowledge_map_create`** — Create a map. Requires `type` (`"roadmap"`) and `title`; optional `folderId` to put it in a folder. Returns the new map, which starts with its root node. **Free plan: 1 map.**
- **`knowledge_map_list`** — List your maps. Returns a summary of each, without its nodes.
- **`knowledge_map_get`** — Get one map with all its nodes. Requires exactly one of `mapId` or `title`.
- **`knowledge_map_rename`** — Rename a map. Requires `mapId` and `title`. Returns the map.
- **`knowledge_map_delete`** — Delete a map. Requires `mapId`. Can't be undone.
- **`knowledge_map_create_folder`** — Create a folder for maps. Requires `title`. Returns the folder.
- **`knowledge_map_rename_folder`** — Rename a folder. Requires `folderId` and `title`. Returns the folder.
- **`knowledge_map_delete_folder`** — Delete a folder. Requires `folderId`. Only an empty folder can be deleted.
- **`knowledge_map_list_folders`** — List your folders.
- **`knowledge_map_move_to_folder`** — Move a map into a folder. Requires `mapId` and `folderId` (`null` takes it out of any folder). Returns the map's summary.
- **`knowledge_map_add_node`** — Add a node. Requires `mapId`, `parentId` and `kind`; optional `label`, `description` and `data`. Returns the map.
- **`knowledge_map_update_node`** — Change a node. Requires `mapId` and `nodeId`; optional `label`, `description`, `data`, and `dataMode` (`merge`, the default, or `replace`). Returns the map.
- **`knowledge_map_delete_node`** — Delete a node. Requires `mapId` and `nodeId`. Can't be undone. Returns the map.
- **`knowledge_map_move_node`** — Move a node under a different parent. Requires `mapId`, `nodeId` and `newParentId`. Returns the map.
- **`knowledge_map_set_node_metrics`** — Set a node's numbers by hand. Requires `mapId`, `nodeId`, and at least one of `progress` (0–100), `cardCount` or `dueCount` (0 or more). Returns the map.
- **`knowledge_map_group`** — Group two or more nodes. Requires `mapId` and `nodeIds` (at least 2); optional `edgeMode` (`merged` or `linked`). Returns the map.
- **`knowledge_map_ungroup`** — Undo a group. Requires `mapId` and `groupId`. Returns the map.
- **`knowledge_map_set_group_edge_mode`** — Change how a group's lines are drawn. Requires `mapId`, `groupId` and `edgeMode`. Returns the map.
- **`knowledge_map_sync_stats`** — Fill in the map's numbers from your real Anki. Requires `mapId`. **Reads your Anki**, so Anki must be running with the add-on. Overwrites the node numbers. Can take a while. Returns the map.

## Media Library

Look up and label your stored pictures, sounds, PDFs and subtitle files. See [Media Library](/docs/anki-studio/media-library/).

There are no tools to upload, delete, move or rename files — you do that in the dashboard.

- **`media_library_read_directory`** — List everything under a folder, subfolders included. Optional `path` (default `/`, the top). Returns each folder and file; for files, the size, type, tags, description and `mediaId`. Changes nothing. **Changed in 0.10.2:** the description now mentions PDFs and subtitle files alongside images and sounds.
- **`media_library_read_file`** — Get one file's details plus a fresh `viewUrl` that works for about 15 minutes. Requires `url_or_path` — a path, a bare `mediaId`, or a link the library gave out earlier (even an expired one). Optional `include_content` (default off): for an image or sound, your AI gets the file itself; for anything else, including PDFs and subtitles, it gets the details and a note saying why the file wasn't included. **Changed in 0.10.2:** the description now covers PDFs and subtitle files, and tells your AI never to paste a `viewUrl` into a card — it stops working when it expires. Use `<img src="ankimcp-media:<mediaId>">` or `[sound:ankimcp-media:<mediaId>]` instead.
- **`media_library_update_file`** — Change a file's tags or description. Requires `path`, plus at least one of `tags` (up to 30, each 1–32 characters) or `description` (up to 2,000 characters). **Writes to the library.**

## Sandbox

Draft cards and preview them before they reach Anki. See [Sandbox](/docs/anki-studio/sandbox/).

Limits: up to **20 cards** per sandbox. In the template, `noteTypeName` is 1–200 characters; `fieldNames` holds 1–50 names of up to 100 characters each; `css` and `js` are up to 256 KB each; `qfmt` and `afmt` (the front and back templates) up to 64 KB each. A card's `fields` are up to 128 KB in total.

Media Library files go in a card as `<img src="ankimcp-media:<mediaId>">` or `[sound:ankimcp-media:<mediaId>]` — in card fields only, not in the template or CSS.

- **`sandbox_get_session`** — Get the template, a short summary of every card, and the card count. Says so if there's no sandbox yet. Saves whatever you're typing in the dashboard editor first, so your AI sees your latest edits.
- **`sandbox_get_cards`** — Get full cards, either by `ids` (1–20) or by page with `offset` and `limit` (1–20) — not both. May return fewer cards than asked if they're large. Saves your open edits first, like `sandbox_get_session`. **Changed in 0.10.2:** the description now says a card that refers to Media Library files must be sent with `sandbox_push_card`, which copies those files into Anki.
- **`sandbox_set_template`** — Replace the whole template. Requires `noteTypeName`, `fieldNames`, `css`, `js`, `qfmt` and `afmt`; optional `createOnly`. This is the only way a sandbox is created. Existing cards are kept.
- **`sandbox_update_template`** — Change part of the template. Requires at least one of `noteTypeName`, `fieldNames`, `css`, `js`, `qfmt` or `afmt`. Fails if there's no sandbox yet.
- **`sandbox_patch_template`** — Find and replace inside one part of the template. Requires `field` (`css`, `js`, `qfmt` or `afmt`), `oldStr` and `newStr`. `oldStr` must match exactly once, and `newStr` must be different.
- **`sandbox_upsert_card`** — Create a card (leave out `id`) or replace a card's fields. Requires `fields`; optional `id`. Returns the card's `id`. **Changed in 0.10.2:** the description now explains how to show a Media Library file in a card, and that such a card must reach Anki through `sandbox_push_card`.
- **`sandbox_patch_card`** — Find and replace inside one field of one card. Requires `id`, `field`, `oldStr` and `newStr` (must be different). **Changed in 0.10.2:** the description now carries the same rule for Media Library files.
- **`sandbox_delete_card`** — Delete one card. Requires `id`. Can't be undone.
- **`sandbox_push_card`** — Add one sandbox card to your Anki as a note. Requires `cardId`, `deck_name` and `model_name`; optional `tags` and `allow_duplicate`. **Adds a note to your Anki** (the add-on, or your Hosted Anki) and returns Anki's reply. **Changed in 0.10.2:** before adding the note, it **copies every Media Library picture and sound the card refers to into Anki's media folder** and points the card at the copies. Only png, jpg, webp, gif, mp3 and wav files are copied. If any file is another type, is missing, or fails to copy, no note is added. Files already copied stay in Anki and are reused next time. No add-on update is needed for this.
- **`sandbox_clear_session`** — Delete the whole sandbox: template and all cards. Can't be undone. Safe to call when there's nothing to clear.

## Text to Speech

Turn text into spoken audio. See [Text to Speech](/docs/anki-studio/text-to-speech/).

Credits per month: **500 on Free, 10,000 on Plus, 30,000 on Pro.**

- **`tts_list_voices`** — List the available voices. Optional `locale` to narrow it down (for example, a language and its regional variants). Returns each voice's name, language, gender and speaking styles.
- **`tts_generate`** — Make an mp3 and save it. Requires `targetFolder` (`""` or `"/"` for the top of the library), `text` (1–5,000 characters), `locale` and `voice`. Optional `fileName` (1–128 characters), `style`, `rate` (−40 to 40) and `pitch` (−30 to 30). Returns the file's path, the credits charged, and your remaining credits. **Costs credits** — Chinese, Japanese and Korean characters count double. **Writes a file to your Media Library.**
- **`tts_get_quota`** — Check your credits: your plan, monthly limit, used this month, and what's left.

## PDF Reader

Read the PDF you have open. See [PDF Reader](/docs/anki-studio/pdf-reader/).

**New in 0.10.2.** These tools read the PDF open in the PDF Reader in your dashboard, in your browser. If nothing is open, they fail. They only read — they can't change your PDF or your notes. You need a PDF project: **1 on Free, unlimited on Plus or Pro** (up to 100). Projects are created in the dashboard, not by your AI.

- **`pdf_reader_status`** — **New in 0.10.2.** Describe the open PDF: the project, the file name, the current page and page count, the zoom, and the PDF's own details (title, author and so on).
- **`pdf_reader_get_page`** — **New in 0.10.2.** Read one page. Requires `page` (1 or more). Optional `format`: `"text"` (the default), `"image"`, or `"pdf"` for a one-page PDF. Optional `annotations` (image only, default off) draws your highlights and markup on the picture.
- **`pdf_reader_list_annotations`** — **New in 0.10.2.** List your highlights, notes, bookmarks, captures and other markup. Optional `pages` (from–to range), `types` (highlight, underline, strikeout, squiggly, ink, square, circle, freetext, note, bookmark, capture, other), `fields` to choose what comes back, `limit` (default 50, max 200) and `offset`.
- **`pdf_reader_get_capture`** — **New in 0.10.2.** Get the saved image of one capture, with its page, date, size and comment. Requires `id`.

## Video Player

Read the video you have open. See [Video Player](/docs/anki-studio/video-player/).

**New in 0.10.2.** These tools read the video project open in the Video Player in your dashboard, in your browser. The video file itself never leaves your computer, so until you open it in the player your AI can't get frames or subtitles — your bookmarks, drawings and captures still work. You need a video project: **1 on Free, unlimited on Plus or Pro** (up to 100). Projects are created in the dashboard, not by your AI.

- **`video_reader_status`** — **New in 0.10.2.** Describe the open project: the file, whether the video is loaded, and if it is, its length, current time, whether it's paused, speed and size. Also the subtitle file, if there is one.
- **`video_reader_get_frame`** — **New in 0.10.2.** Get one frame as a picture: the current one, the one at `time` (seconds), or the one showing an annotation (`annotationId`) — `time` and `annotationId` can't be combined. With `annotationId`, optional `view` (`"crop"` or `"overlay"`). Without it, optional `annotations` draws your markup on the frame. **With `time` or `annotationId`, it briefly seeks your video there and back.**
- **`video_reader_get_subtitles`** — **New in 0.10.2.** Get subtitle lines with their start and end times. Optional `time` (from–to range), `limit` (default 100, max 500) and `offset`.
- **`video_reader_list_annotations`** — **New in 0.10.2.** List your bookmarks, spans, drawings, captures and other markup. Optional `time` (from–to range), `types` (bookmark, range, rect, freehand, text, arrow, ellipse, capture, other), `fields`, `limit` (default 50, max 200) and `offset`.
- **`video_reader_get_capture`** — **New in 0.10.2.** Get the saved image of one capture, with its time, date, size and comment. Requires `id`.

## What your AI sees when something is off

| Situation | What your AI gets |
|---|---|
| Free plan, already has a knowledge map, tries `knowledge_map_create` | `TIER_LIMIT_REACHED` |
| A reader tool, but the dashboard or the document isn't open | "No PDF or video is open in the studio Reader. Open a PDF or video project in the Reader page first." |
| A `pdf_reader_*` tool while a video is open (or the other way round) | "The studio Reader has a video open, which this tool does not read. Use the `video_reader_*` tools for it." |
| A frame or subtitles before the video file is opened in the player | `NO_MEDIA` — "The project is open but its video file is not loaded yet; ask the user to open the file in the Reader." |
| A reader result that's too big to send, even after shrinking images | `TOO_LARGE` |

## Keeping the tool list fresh

Claude, ChatGPT and other clients remember the tool list from when you added Studio. When Studio gains tools, they won't show up until you remove the Studio connector and add it again. Your existing connection keeps working in the meantime — nothing it already knows was removed or renamed.

---

*Disclaimer: "Anki" is a registered trademark of Ankitects Pty Ltd. AnkiMCP is an independent, community-built project and is **not** affiliated with, endorsed by, or sponsored by Ankitects. MCP is an open standard originated by Anthropic; AnkiMCP is likewise not affiliated with or endorsed by Anthropic.*
