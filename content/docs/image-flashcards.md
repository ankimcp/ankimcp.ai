---
title: "Add Images to Anki Flashcards with AI - Visual Learning Cards"
linkTitle: "Image Flashcards"
description: "Learn how to efficiently add images to your Anki flashcards using AI assistants. Avoid slow base64 conversion and use file paths or URLs for instant image uploads."
keywords: ["anki image flashcards", "add images to anki", "visual flashcards", "anki mcp images", "ai image cards"]
weight: 28
toc: true
---

Learn how to add images to your Anki flashcards efficiently using Anki MCP's `mediaActions` tool.

## Overview

Anki MCP's `mediaActions` tool lets you upload, manage, and delete image files in your Anki collection. You can add diagrams, photos, charts, screenshots, and any other visual content to enhance your flashcards.

## Prerequisites

1. **Anki MCP installed** - Follow the [installation guide](/docs/installation)
2. **Anki running** with AnkiConnect plugin
3. **Optional but recommended:** [Filesystem MCP](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem) for Claude Desktop users

## Three Methods to Add Images

### Method 1: URL (Recommended for Web Images) ✅

Best for images already on the internet.

**Example conversation:**
```
User: Add this diagram to my physics card: https://example.com/diagram.png

AI: [Uses mediaActions to download and store]
    ✓ Successfully stored media file: diagram.png
    [Creates or updates card with <img src="diagram.png">]
```

**Behind the scenes:**
```javascript
mediaActions({
  action: "storeMediaFile",
  filename: "diagram.png",
  url: "https://example.com/diagram.png"
})
```

**Benefits:**
- Zero tokens used (AI doesn't process the image)
- Anki downloads directly from the URL
- Instant, efficient processing

### Method 2: File Path (Recommended for Local Files) ✅

Best for images saved on your computer.

**Example conversation:**
```
User: Add the image cat.jpg from my Desktop to this card

AI: [Uses Filesystem MCP to locate: /Users/username/Desktop/cat.jpg]
    [Uses mediaActions to upload]
    ✓ Successfully stored media file: cat.jpg
    [Adds <img src="cat.jpg"> to card]
```

**Behind the scenes:**
```javascript
mediaActions({
  action: "storeMediaFile",
  filename: "cat.jpg",
  path: "/Users/username/Desktop/cat.jpg"
})
```

**Benefits:**
- Zero tokens used
- Efficient processing
- Works with local screenshots, downloads, photos

**Requirements:**
- **Claude Desktop:** Enable Filesystem MCP extension for automatic file location
- **Without Filesystem MCP:** Provide full path manually (e.g., `/Users/yourname/Desktop/image.jpg`)
- **Other MCP clients:** Configure filesystem access in your client

### Method 3: Base64 (NOT Recommended) ❌

When you paste images directly into Claude.

**What happens:**
```
User: [Pastes image into Claude]
      Add this image to my card

AI: [Claude converts image to base64 - a huge text string]
    [This can take 30+ seconds even for small images]
    [Uses thousands of tokens]
```

**Why to avoid:**
- ⚠️ Even 4kb images are extremely slow
- ⚠️ Wastes thousands of tokens (expensive)
- ⚠️ Large images may fail or timeout
- ⚠️ Poor user experience

**Better approach:**
1. Save the pasted image to your computer first
2. Then use Method 2 (file path)

## Basic Workflow

### Step 1: Prepare Your Image

Choose one:
- **Web image:** Copy the URL
- **Local image:** Save to your computer (Desktop, Downloads, Pictures)
- **Screenshot:** Save to a known location

### Step 2: Upload to Anki

Tell the AI where the image is:

```
"Add https://example.com/diagram.png to my card"
```

or

```
"Add the image biology-cell.png from my Downloads folder"
```

### Step 3: Create or Update Card

The AI will create a card with the image:

```
Create a flashcard in "Biology" deck:
- Front: What is this cell structure? <img src="biology-cell.png">
- Back: Mitochondria - the powerhouse of the cell
```

### Step 4: Study

Open Anki and study your deck. The image will display on your card!

## Conversation Examples

### Example 1: Web Image

```
User: Create a flashcard about the Eiffel Tower with this image:
      https://upload.wikimedia.org/wikipedia/commons/thumb/a/a8/Tour_Eiffel_Wikimedia_Commons.jpg/800px-Tour_Eiffel_Wikimedia_Commons.jpg

AI: I'll create a flashcard with that image.
    [Uses mediaActions to download and store as eiffel_tower.jpg]
    ✓ Successfully stored media file: eiffel_tower.jpg

    [Uses addNote to create card]
    ✓ Successfully created note in deck "Geography"
    Front: <img src="eiffel_tower.jpg">
    Back: The Eiffel Tower in Paris, France. Built in 1889, stands 330m tall.
```

### Example 2: Local Screenshot

```
User: I just took a screenshot of a Python error.
      It's on my Desktop as python_error.png
      Create a troubleshooting card with it

AI: [Uses Filesystem MCP to locate: /Users/username/Desktop/python_error.png]
    [Uses mediaActions to upload]
    ✓ Successfully stored media file: python_error.png

    [Uses addNote]
    ✓ Successfully created note in deck "Programming"
    Front: What's wrong with this code? <img src="python_error.png">
    Back: IndexError: list index out of range - accessing beyond list length
```

### Example 3: Batch Upload

```
User: Add these anatomy diagrams to my Medical School deck:
      1. https://example.com/heart.png
      2. https://example.com/lungs.png
      3. https://example.com/brain.png

AI: [Downloads all 3 images using mediaActions]
    ✓ Successfully stored: heart.png
    ✓ Successfully stored: lungs.png
    ✓ Successfully stored: brain.png

    [Creates 3 flashcards]
    ✓ Created 3 anatomy cards in "Medical School"
```

## Best Practices

### File Naming

Use descriptive, consistent names:

✅ **Good:**
- `biology_cell_mitochondria.png`
- `spanish_verb_conjugation_chart.jpg`
- `math_pythagorean_theorem_diagram.png`

❌ **Bad:**
- `image1.png`
- `screenshot.png`
- `temp.jpg`

### Organize with Prefixes

Group related images:

```
biology_cell_nucleus.png
biology_cell_mitochondria.png
biology_cell_membrane.png
spanish_map_spain.jpg
spanish_map_latin_america.jpg
```

Search by category:
```
List all media files matching "biology_cell_*.png"
```

### Prevent Automatic Cleanup

Prefix with underscore to prevent Anki's media cleanup:

```
_reference_periodic_table.png
```

Files starting with `_` won't be deleted when you run "Check Media" in Anki.

### Reuse Images

Reference the same image in multiple cards:

```
Card 1: <img src="cell.png"> What is structure A?
Card 2: <img src="cell.png"> What is structure B?
Card 3: <img src="cell.png"> Label all parts
```

## Troubleshooting

### Images Loading Slowly

**Problem:** Claude takes forever to process images.

**Solution:**
- Don't paste images directly into Claude
- Use URL or file path methods instead
- Enable Filesystem MCP for Claude Desktop

### Image Not Showing in Anki

**Check:**
1. Image was uploaded: Look in Anki's media folder
2. Filename matches: `<img src="filename.jpg">` uses exact filename
3. Sync if using AnkiWeb

### File Path Not Found

**For Claude Desktop:**
- Enable Filesystem MCP extension
- Configure access to relevant folders (Desktop, Downloads, Pictures)

**Manual path entry:**
- Use full absolute path: `/Users/yourname/Desktop/image.jpg`
- Check spelling and spaces in filename

### Large Images Breaking

**Solutions:**
- Resize images before uploading (use image editor)
- Compress JPEG images (reduce quality slightly)
- Use PNG only for diagrams/screenshots, JPEG for photos
- Keep images under 2MB if possible

## Setup: Filesystem MCP for Claude Desktop

To enable automatic file location:

1. **Open Claude Desktop**
2. **Settings → Extensions**
3. **Browse catalog** → Find "Filesystem MCP"
4. **Install** the extension
5. **Configure** access to folders:
   - Desktop
   - Downloads
   - Pictures
   - Any other folders with images

**Benefits:**
- Claude can automatically find images you mention
- No need to type full file paths
- Faster workflow

**Example:**
```
User: Add the screenshot from my Desktop

AI: [Automatically searches Desktop folder]
    Found: screenshot_2024-01-15.png
    [Uploads to Anki]
```

## Video Tutorial

Watch a demonstration of adding images to Anki cards:

[![Image Upload Demo](https://img.youtube.com/vi/8pcOjfmD4ng/maxresdefault.jpg)](https://www.youtube.com/watch?v=8pcOjfmD4ng)

---

**Need help?** Check the [FAQ](/docs/faq) or visit our [Getting Help](/docs/getting-help) page.