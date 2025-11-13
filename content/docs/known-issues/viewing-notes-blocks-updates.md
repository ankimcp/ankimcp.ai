---
title: "Silent Note Update Failure"
linkTitle: "Silent Note Update Failure"
description: "Note updates may silently fail when the note is open in Anki's browser window - a known AnkiConnect API limitation"
sitemap_priority: 0.6
weight: 10
keywords: ["anki browser", "update fails", "silent failure", "ankiconnect limitation", "note not saving", "updates don't work"]
---

## The Problem

When you have a note open in Anki's **browser window**, any updates attempted through your AI assistant **may silently fail**. The AI assistant will report success, but your changes won't actually save to the note.

## Example Scenario

1. You open Anki and browse to a specific note (e.g., searching for "photosynthesis")
2. The note is now displayed in Anki's browser window
3. You ask your AI to update that same note
4. AI reports "done!" but the note remains unchanged
5. No error message appears - it just silently fails

## Why This Happens

The [AnkiConnect API documentation](https://git.sr.ht/~foosoft/anki-connect#codeupdatenotefieldscode) explicitly states:

> "You must not be viewing the note that you are updating on your Anki browser, otherwise the fields will not update"

See [this issue](https://github.com/FooSoft/anki-connect/issues/82) for further details.

## The Solution

**Ensure the note is not selected or being viewed in Anki's browser before updating it through your AI assistant.**

### How to avoid this issue:

1. **If viewing a note**: Either:
   - Close the Anki browser window entirely, OR
   - Click on a different note to deselect the current one, OR
   - Press Escape to deselect without closing
2. **Then**: Ask your AI assistant to make updates
3. **Finally**: Open the browser again to verify changes

## Why We Can't Auto-Fix This

Currently, AnkiConnect doesn't provide:
- A way to detect if a note is being viewed in the browser
- A method to close or deselect notes programmatically
- An error response when updates are blocked

This means user awareness is the best solution for now.

## Status

**Under Investigation** - We're actively exploring solutions to improve this experience. For now, simply closing or switching away from the note in Anki's browser ensures updates work correctly.

## Related Links

- [AnkiConnect Issue #82](https://github.com/FooSoft/anki-connect/issues/82) - Original bug report
- [AnkiConnect Documentation](https://git.sr.ht/~foosoft/anki-connect) - Official API documentation

---

*Last Updated: November 2025*