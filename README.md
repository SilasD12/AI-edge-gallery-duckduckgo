# Deep Web Research — Google AI Edge Skill

A skill for the [Google AI Edge Gallery](https://github.com/google-ai-edge/ai-edge-gallery) app that gives the on-device Gemma model real-time access to the web. When the model's training data may be out of date or insufficient, this skill searches **DuckDuckGo** and **Wikipedia** in parallel and returns sourced, up-to-date information — no API key required.

## What it does

| Source | What it fetches |
|--------|----------------|
| **DuckDuckGo Instant Answers** | Quick answers, abstracts, definitions, and related topics |
| **Wikipedia** | Article intro text and infobox key/value pairs, in the user's language |

The model receives the combined results and synthesizes them into a concise, cited response.

## When the model uses this skill

The model invokes this skill automatically for:

- Current events or time-sensitive information
- Specific people, places, organizations, or historical events
- Definitions, statistics, or factual data where accuracy matters
- Anything that may have changed after the model's training cutoff

It does **not** use this skill for personal advice, creative writing, math, coding, or casual conversation.

## Installation in Google AI Edge Gallery

This skill is hosted via GitHub Pages. No downloading or file transfer needed — add it directly by URL.

### One-time setup: enable GitHub Pages

If you haven't already, go to the **AI-edge-gallery-duckduckgo** repo settings:

- **Settings → Pages → Source:** `main` branch, `/ (root)`
- Make sure a `.nojekyll` file exists in the repo root so GitHub Pages serves `SKILL.md` as raw text (not rendered HTML)

Once Pages is enabled, the skill URL is:

```
https://<your-username>.github.io/AI-edge-gallery-duckduckgo/deep-web-research
```

### Adding the skill to the app

1. **Open AI Edge Gallery** on your device and select your Gemma model
2. Enter the **Agent Skills** use case
3. Tap the **Skills** chip → tap **(+)**
4. Choose **"Load skill from URL"**
5. Enter the URL above (with your actual GitHub username)
6. Confirm — the skill will appear in your skill list immediately

### Verify the URL is working

Before adding it in the app, you can check that the URL is correct by opening this in a browser — it should display raw markdown text:

```
https://<your-username>.github.io/AI-edge-gallery-duckduckgo/deep-web-research/SKILL.md
```

### Start chatting

Select a Gemma model in the app and ask about any current event or factual topic. The model will invoke the skill automatically when it detects the query benefits from live web data.

## File structure

```
gemma4-skills/
├── SKILL.md          # Skill metadata and instructions for the model
└── scripts/
    └── index.html    # Skill runtime (HTML/JS executed by the app's WebView)
```

## How it works (technical)

The AI Edge Gallery app exposes a `run_js` tool that loads a local HTML file in an isolated WebView and calls `window.ai_edge_gallery_get_result(data)` with a JSON string. This skill implements that function to:

1. Parse `query`, `topic`, and `lang` from the JSON input.
2. Fetch DuckDuckGo Instant Answers and Wikipedia data **in parallel**.
3. Return a combined JSON string `{ result: "..." }` (or `{ error: "..." }` on failure).

The Wikipedia fetch is language-aware — pass `"lang": "es"` for Spanish results, `"lang": "ja"` for Japanese, etc.

## Requirements

- iOS or Android device with **AI Edge Gallery** installed
- Internet access on the device at query time
- No API keys or accounts needed
