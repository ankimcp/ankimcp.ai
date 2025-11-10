---
title: "Create AI Audio Flashcards for Anki - Voice & Pronunciation Cards"
linkTitle: "Audio Flashcards"
description: "Generate native pronunciation audio with AI voice services like ElevenLabs and embed directly into Anki flashcards. Perfect for language learning."
keywords: ["anki audio flashcards", "ai voice flashcards", "elevenlabs anki", "pronunciation cards", "language learning anki"]
weight: 30
toc: true
---

Learn how to create flashcards with audio content using Anki MCP's `mediaActions` tool in combination with audio-generating MCP servers.

## Overview

Anki MCP's `mediaActions` tool lets you upload, manage, and delete audio files in your Anki collection. When combined with MCP servers that generate audio (like text-to-speech services), you can create rich audio flashcards for language learning, pronunciation practice, and more.

## Prerequisites

1. **Anki MCP installed** - Follow the [installation guide](/docs/installation)
2. **Anki running** with AnkiConnect plugin
3. **An audio-generating MCP server** - Examples:
   - [ElevenLabs MCP](https://github.com/elevenlabs/elevenlabs-mcp) - High-quality TTS in 29+ languages
   - Any other MCP server that can generate or provide audio files

## Basic Workflow

The typical workflow involves three steps:

### Step 1: Generate Audio

Use an audio-generating MCP server to create your audio file. For example, with a text-to-speech service:

```
Generate Spanish audio for "Buenos días" and save it as buenos_dias.mp3
```

The audio MCP server creates the file locally or provides it as base64 data.

### Step 2: Upload to Anki

Use Anki MCP's `mediaActions` tool to upload the audio:

```
Upload buenos_dias.mp3 to Anki
```

Behind the scenes, this calls:
```javascript
mediaActions({
  action: "storeMediaFile",
  filename: "buenos_dias.mp3",
  data: "base64_encoded_audio_data..."  // or path/url
})
```

The file is stored in Anki's media collection folder.

### Step 3: Create Flashcard with Audio Reference

Create a note that references the audio file:

```
Create a flashcard in "Spanish Vocabulary" deck:
- Front: [sound:buenos_dias.mp3]
- Back: Good morning
```

The `[sound:filename.mp3]` syntax tells Anki to display an audio player.

### Step 4: Study

Open Anki and study your deck. Click the play button to hear the audio!

## Conversation Examples

### Example 1: Simple Audio Card

```
User: Generate French audio for "Bonjour" using a native speaker voice

AI: [Uses audio MCP server to generate bonjour.mp3]
    Audio generated successfully: bonjour.mp3

User: Upload it to Anki

AI: [Uses mediaActions to upload]
    ✓ Successfully stored media file: bonjour.mp3

User: Create a flashcard with this audio in my French deck

AI: [Uses addNote]
    ✓ Successfully created note in deck "French"
    Front: [sound:bonjour.mp3]
    Back: Hello, Good morning
```

### Example 2: Batch Creation

```
User: Generate Spanish audio for these phrases:
      1. "Hola" → hola.mp3
      2. "Gracias" → gracias.mp3
      3. "Por favor" → por_favor.mp3

      Upload all to Anki and create flashcards in "Spanish Basics" deck

AI: [Generates 3 audio files]
    [Uploads all 3 using mediaActions]
    [Creates 3 flashcards using addNote]

    ✓ Created 3 audio flashcards in "Spanish Basics":
    1. hola.mp3 → "Hello"
    2. gracias.mp3 → "Thank you"
    3. por_favor.mp3 → "Please"
```

### Example 3: Audio Management

```
User: List all my Spanish audio files

AI: [Uses getMediaFilesNames with pattern "spanish_*.mp3"]
    Found 15 files:
    - spanish_hello.mp3
    - spanish_thanks.mp3
    - spanish_goodbye.mp3
    ...

User: Delete spanish_old_version.mp3

AI: [Uses deleteMediaFile]
    ✓ Successfully deleted media file: spanish_old_version.mp3
```

## Advanced: Custom Audio Note Types

For better audio learning experiences, create a custom note type optimized for audio-first learning.

### Audio-First Learning Model

**Ask your AI:**
```
Create a new Anki model called "Audio Learning" with these fields:
- Audio: filename only (e.g., "spanish_audio.mp3")
- Text: original phrase in target language
- Translation: translation in my native language

Front template: large green play button, centered, no autoplay
Back template: show front + text + translation
```

**Example front template:**
```html
<div style="text-align: center; padding: 20px;">
  <button onclick="var audio = document.createElement('audio');
    audio.src='{{Audio}}'; audio.play(); return false;"
    style="font-size: 36px; padding: 15px 30px;
    background: #4CAF50; color: white; border: none;
    border-radius: 8px; cursor: pointer;">
    ▶️ Listen
  </button>
</div>
```

**Example back template:**
```html
{{FrontSide}}
<hr id="answer">
<div style="font-size: 28px; margin: 20px;">{{Text}}</div>
<div style="font-size: 18px; color: #666;">
  <b>Translation:</b> {{Translation}}
</div>
```

**Benefits:**
- Audio-first approach: listen before reading
- Active engagement: click to play (no autoplay)
- Clean, distraction-free interface
- Progressive reveal: audio → text → translation

## Best Practices

### File Naming Conventions

Use descriptive, consistent filenames:

✅ **Good:**
- `spanish_hello_formal.mp3`
- `french_verb_aller.mp3`
- `japanese_greeting_casual.mp3`

❌ **Bad:**
- `audio1.mp3`
- `temp.mp3`
- `file.mp3`

### Prevent Automatic Cleanup

Prefix filenames with underscore to prevent Anki's automatic media cleanup:

```
Upload as _spanish_hello.mp3
```

Files starting with `_` won't be deleted when you run "Check Media" in Anki.

### Organize with Prefixes

Use consistent prefixes for related content:

```
spanish_greetings_hello.mp3
spanish_greetings_goodbye.mp3
spanish_food_water.mp3
spanish_food_bread.mp3
```

This makes it easy to list related files:
```
List all media files matching "spanish_greetings_*.mp3"
```

### Reuse Audio Files

The same audio file can be referenced in multiple flashcards:

```
Card 1: [sound:hello.mp3] → "Hello"
Card 2: [sound:hello.mp3] + "in the morning" → "Good morning greeting"
Card 3: "When to use: [sound:hello.mp3]" → "Informal situations"
```

### Check Before Uploading

Avoid duplicates by checking existing files:

```
List media files matching "spanish_hello*.mp3"

If exists, use spanish_hello_v2.mp3 instead
```

## Use Cases

### Language Learning

**Pronunciation Practice:**
- Upload native speaker audio
- Create cards with audio on front
- Text and translation on back
- Practice listening comprehension

**Conversation Dialogs:**
- Multi-turn conversations with different voices
- Question audio on front
- Answer audio + translation on back

### Vocabulary Building

**Context-based Learning:**
- Sentence audio showing word usage
- Isolated word audio for pronunciation
- Translation and usage notes

### Music Education

**Chord Progressions:**
- Audio examples of different progressions
- Identify by ear exercises

**Rhythm Patterns:**
- Audio clips of rhythm examples
- Notation on back

### Accessibility

**Audio Descriptions:**
- Audio explanations for visual concepts
- Text-to-speech for any content
- Multi-modal learning for different learning styles

## Example Audio MCP Servers

### ElevenLabs MCP
- **Repository:** [github.com/elevenlabs/elevenlabs-mcp](https://github.com/elevenlabs/elevenlabs-mcp)
- **Features:** High-quality TTS, 29+ languages, multiple voices
- **Best for:** Professional-quality language learning content

### Other Options
- Custom TTS servers built with MCP SDK
- Local TTS solutions (piper, coqui-tts, etc.)
- Any MCP server that can generate or serve audio files

---

**Note:** Audio-generating MCP servers are separate projects. Check their documentation for setup instructions and API requirements.
