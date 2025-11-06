---
title: "AI Prompts for Better Anki Flashcards - Twenty Rules & Best Practices"
linkTitle: "Using Prompts"
description: "Optimize flashcard creation with built-in AI prompts following the Twenty Rules of Knowledge Formulation. Create more effective cards that improve retention."
keywords: ["anki ai prompts", "twenty rules anki", "flashcard best practices", "ai study prompts", "anki formulation rules"]
weight: 25
---

Anki MCP includes built-in prompts that guide AI assistants on how to help you create better flashcards and conduct effective study sessions.

## What Are Prompts?

Prompts are pre-written instructions that tell the AI assistant how to approach specific tasks. When you activate a prompt, the AI receives detailed guidance on best practices, workflows, and principles to follow.

Think of prompts as expert coaching for your AI assistant - they ensure consistent, high-quality help every time.

## Available Prompts

### 📝 anki_review

**Purpose:** Guides the AI through interactive review sessions

This prompt helps the AI:
- Present cards one at a time without spoiling answers
- Wait for your response before revealing the answer
- Explain concepts when you get stuck
- Adapt to your learning pace
- Track your progress through the session

**Best for:**
- Daily review sessions
- Catching up on due cards
- Focused study time

**How to use:**
1. Click the attachment button (+) in the input field
2. Select "Add from Anki MCP Server"
3. Choose "Anki review" from the list
4. Tell Claude which deck you want to review

**Example:**
```
You: *Activates anki_review prompt*
You: "Let's review my Spanish deck"

Claude: I'll help you review your Spanish deck. Let me get your due cards...
[Shows first card question]
What's your answer?

You: [Your answer]

Claude: [Reveals answer and provides feedback]
Rate this card: Again / Hard / Good / Easy
```

### 🧠 twenty_rules

**Purpose:** Applies evidence-based principles for creating effective flashcards

Based on Dr. Piotr Wozniak's "Twenty Rules of Formulating Knowledge" from SuperMemo research, this prompt ensures your flashcards are optimized for long-term retention.

**Key principles applied:**
- **Simplicity** - One concept per card
- **Clarity** - Unambiguous questions
- **Atomicity** - Break complex topics into simple pieces
- **Mnemonics** - Memory techniques and associations
- **Optimization** - Perfect wording for spaced repetition

**Best for:**
- Creating new flashcards from learning materials
- Converting notes or textbooks into cards
- Studying for exams
- Language learning
- Professional certifications

**How to use:**
1. Click the attachment button (+) in the input field
2. Select "Add from Anki MCP Server"
3. Choose "Twenty rules" from the list
4. Provide the material you want to learn

**Example:**
```
You: *Activates twenty_rules prompt*
You: "Help me create flashcards about the French Revolution"

Claude: I'll help you create effective flashcards following evidence-based
principles. Let's break down the French Revolution into atomic, memorable cards.

[Creates optimized flashcard sets with clear questions, simple answers,
and mnemonic devices where appropriate]
```

## How Prompts Work

### In Claude Desktop

**Step 1: Click the attachment button (+)**

![Click the plus button](/images/adding-prompt/prompt1.png)

**Step 2: Open "Add from Anki MCP Server"**

![Select Anki MCP Server](/images/adding-prompt/prompt2.png)

**Step 3: Select your prompt**

You'll see available prompts including "Twenty rules" and "Anki review".

![Choose prompt](/images/adding-prompt/prompt3.png)

**Step 4: Start working**

The prompt content is attached to your conversation. Claude now has the guidance it needs!

![Prompt attached](/images/adding-prompt/prompt4.png)

**What happens next:**
- Tell Claude what you want to do
- The AI follows the prompt's instructions automatically
- Continue chatting naturally - the guidance persists throughout the conversation
- You can attach different prompts anytime by repeating the process

## Research and References

The `twenty_rules` prompt is based on:

**"Twenty Rules of Formulating Knowledge"** by Dr. Piotr Wozniak
- Creator of SuperMemo (the algorithm behind Anki)
- Pioneer in spaced repetition research
- Decades of empirical research on memory formation

**Read the original article:**
→ [supermemo.com/en/blog/twenty-rules-of-formulating-knowledge](https://www.supermemo.com/en/blog/twenty-rules-of-formulating-knowledge)

## Feedback and Suggestions

Have ideas for new prompts? Let us know!

- [GitHub Discussions](https://github.com/anki-mcp/anki-mcp-desktop/discussions)
- [Discord Server](https://discord.gg/JVNcxNB3e7)
- [Email Us](mailto:support@ankimcp.ai)
