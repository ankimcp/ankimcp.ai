---
title: "The Twenty Rules of Formulating Knowledge: How to Write Anki Cards That Stick"
linkTitle: "The twenty rules"
description: "Dr. Piotr Wozniak's twenty rules for writing flashcards, explained in plain words with Anki examples, and how AnkiMCP's twenty_rules prompt applies them for you."
keywords:
  - twenty rules of formulating knowledge
  - 20 rules anki
  - how to make good anki cards
  - minimum information principle
  - anki card writing rules
  - wozniak twenty rules
  - effective flashcards
  - anki cloze deletion tips
weight: 8
sitemap_priority: 0.8
---

**A flashcard works when it asks for one small, clear fact that you already understand.** That is the heart of the "Twenty Rules of Formulating Knowledge," written in 1999 by Dr. Piotr Wozniak, the creator of SuperMemo, the program whose scheduling ideas Anki is built on. Spaced repetition decides *when* you review. These rules decide *what* you review, and a badly written card wastes every review it gets.

This page explains the rules in plain words, with examples you can copy. If you use AnkiMCP, the built-in `twenty_rules` prompt hands these rules to your AI, so the cards it writes follow them without you having to remember them. [How to attach it](#how-ankimcp-applies-the-rules-for-you) is at the end.

## Why card quality matters more than review schedule

[Spaced repetition works](/docs/concepts/power-of-anki/) because each review pulls a memory back right before it fades. But the card decides what gets pulled. A card that holds five facts gets rated "Again" because you missed one of them, and all five come back tomorrow. A card that holds one fact gets rated honestly, and Anki schedules it right.

Wozniak's rules all point the same way: make the card small, make it clear, and make it yours. Here they are, grouped by what they fix.

## Before you write a single card

**1. Do not learn if you do not understand.** A card about something you don't understand is a card you'll memorize as noise. Read the explanation first. If you can't explain the fact in your own words, you're not ready to make a card for it.

**2. Learn before you memorize.** Get the big picture before the details. Before cards about individual Spanish verb endings, know that Spanish verbs come in three groups. The overview gives every detail a place to hang.

**3. Build upon the basics.** Simple before complex. Cards about fractions before cards about algebra. Basic cards feel too easy, and that's fine: they're cheap to review and they hold up everything above them.

**20. Prioritize.** Not every fact deserves a card. Ask: will I actually need to recall this? Five cards you need beat fifty you don't. (Wozniak lists this last, but it's the first question to ask.)

## The one rule that matters most

**4. Stick to the minimum information principle.** One card, one fact. This is the rule people break most, and the one that pays off most.

Too much on one card:

```
Q: What is photosynthesis?
A: A process where plants use sunlight, water, and CO2 to make
   glucose and oxygen in the chloroplasts.
```

Split into atomic cards:

```
Q: What are the three inputs of photosynthesis?
A: Sunlight, water, carbon dioxide

Q: What are the two products of photosynthesis?
A: Glucose and oxygen

Q: Where in the plant cell does photosynthesis happen?
A: In the chloroplasts
```

Simple cards are reviewed in seconds, rated honestly, and scheduled right. Complex cards get rated "Again" over and over because one piece slipped.

## Pick a format that makes the card easy

**5. Cloze deletion is easy and effective.** A cloze card is a sentence with a blank. It's the fastest way to turn a fact into a card, and Anki supports it natively with the Cloze note type.

```
The capital of {{c1::France}} is {{c2::Paris}}.
```

That one note makes two cards, each hiding one blank. Cloze is ideal for facts, definitions, and relationships.

**6. Use imagery.** Visual memory is strong. For geography, anatomy, art, or diagrams, a picture on the card beats a paragraph. See [Add images to cards](/docs/how-to/add-images-to-cards/).

**8. Graphic deletion is as good as cloze deletion.** Hide a label on a diagram instead of a word in a sentence. Anki's image occlusion note type does exactly this.

**7. Use mnemonic techniques.** Memory tricks are not cheating. "PEMDAS" for order of operations, a vivid image for an abstract term. If a card keeps failing, add a hook.

## Avoid the card types that fail

**9. Avoid sets.** A card that asks "List all the US state capitals" will never be learned. Make one card per item, or use cloze deletion with context.

**10. Avoid enumerations.** Ordered lists are only slightly better than sets. If the order matters, use a cloze with overlapping blanks, keep the list short, and add a cue: "The first stage of the water cycle is {{c1::evaporation}}."

**11. Combat interference.** Two cards that look alike get mixed up. "Capital of Guyana?" and "Capital of Suriname?" will fight each other for months. Add a distinguishing detail to each: "Capital of Guyana, the only English-speaking country in South America?"

## Make the wording work for you

**12. Optimize wording.** Shorter is better. Remove every word that isn't needed to make the question unambiguous.

Before: *"In the context of programming, when considering the various paradigms, what would you say is the main characteristic that defines the functional approach?"*

After: *"Functional programming's main characteristic?"*

**16. Context cues simplify wording.** A prefix tells you what the question is about so the question itself can be short. "js: array method for filtering?" is clearer than a full sentence, and the "js:" also stops it interfering with a similar Python card. Tags and decks do the same job.

**17. Redundancy does not contradict the minimum information principle.** Testing the same fact from two angles is fine. "Paris is the capital of ___?" and "___ is the capital of France" are both useful. Just don't let it become clutter.

## Connect the card to your own memory

**13. Refer to other memories.** Link a new fact to one you already hold. "Like REST, but with a single endpoint: {{c1::GraphQL}}." The old memory becomes a handle for the new one.

**14. Personalize and provide examples.** A card about a TypeScript interface sticks better if it mentions the one from your own project. Your own examples are the strongest cues you have.

**15. Rely on emotional states.** Dry facts fade; stories stay. A date lands better with the drama around it. Don't overdo it, but a little vividness goes a long way.

## Keep the card maintainable

**18. Provide sources.** Put the page number, URL, or book in an extra field. Six months on, when the card seems wrong, you'll want to check.

**19. Provide date stamping.** For facts that change, such as prices, versions, or office holders, note when the card was written. Then you know when to trust it.

## How AnkiMCP applies the rules for you

Remembering twenty rules while you write cards is hard. Remembering them while an AI writes cards for you is easier: the AI holds the rules, you hold the topic.

AnkiMCP ships a built-in `twenty_rules` prompt. Attach it in Claude, then ask for cards on any topic. The prompt tells Claude to check you understand the material, split everything into one-fact cards, prefer cloze for facts, keep wording short, add context cues, and show you the proposed cards before adding them to Anki.

Without the prompt, an AI tends to write cards like the first photosynthesis example above: a question, then a paragraph. With it, you get the second example. See [AI prompts for flashcards](/docs/how-to/anki-ai-prompts/) for how to attach it, and [PDF to Anki](/docs/how-to/pdf-to-anki/) for a full walkthrough that uses it.

The prompt is tuned for Anki and AI chat, so it's not a word-for-word copy. Two of Wozniak's rules, graphic deletion (8) and date stamping (19), are left to you, because they depend on your images and your subject. The other eighteen are in the prompt.

## Further reading

- [Twenty Rules of Formulating Knowledge](https://www.supermemo.com/en/blog/twenty-rules-of-formulating-knowledge), Dr. Piotr Wozniak's original 1999 article.
- [The Power of Anki](/docs/concepts/power-of-anki/), why spaced repetition and active recall work.
- [AI prompts for flashcards](/docs/how-to/anki-ai-prompts/), how to use the built-in prompts.

---

*Disclaimer: "Anki" is a registered trademark of Ankitects Pty Ltd. AnkiMCP is an independent, community-built project and is **not** affiliated with, endorsed by, or sponsored by Ankitects. SuperMemo is a trademark of SuperMemo World; AnkiMCP is not affiliated with SuperMemo World or Dr. Wozniak.*
