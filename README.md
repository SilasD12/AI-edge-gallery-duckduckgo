# Deep Web Research — AI Edge Gallery Skill

A skill for the [Google AI Edge Gallery](https://github.com/google-ai-edge/gallery) app that gives your on-device Gemma model real-time access to the web. When a query needs current or factual information, the model fetches from **DuckDuckGo** and **Wikipedia** in parallel and synthesizes a sourced answer — no API key required.

## Install

Open **AI Edge Gallery** → Agent Skills → **Skills** chip → **(+)** → **Load skill from URL**:

```
https://SilasD12.github.io/AI-edge-gallery-duckduckgo
```

## What it fetches

| Source | Data |
|--------|------|
| **DuckDuckGo Instant Answers** | Quick answers, abstracts, definitions, related topics |
| **Wikipedia** | Article intro and infobox facts, in the user's language |

## Usage

Just ask naturally — the model invokes this skill automatically when it detects a query that benefits from live data:

- *"Who won the 2025 Nobel Prize in Physics?"*
- *"What is the population of Tokyo?"*
- *"Tell me about the James Webb Space Telescope"*
- *"What happened at the 2026 Oscars?"*

It does not trigger for personal advice, creative writing, math, or casual conversation.

## Language support

Pass queries in any language — the Wikipedia lookup is language-aware and will return results in the user's language (English, Spanish, French, German, Japanese, Korean, Chinese, Portuguese, Arabic, Hindi, and more).

## How it works

The AI Edge Gallery app loads `scripts/index.html` in a sandboxed WebView and calls `window.ai_edge_gallery_get_result(data)` with a JSON payload from the model. The script runs both fetches in parallel via `Promise.all`, combines the results, and returns them to the model for synthesis.

No API keys. No accounts. Works anywhere you have a data connection.
