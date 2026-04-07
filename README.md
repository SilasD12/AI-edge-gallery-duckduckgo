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

Follow these steps to sideload the skill into the AI Edge Gallery Android app:

1. **Download the skill file**
   - Get `scripts/index.html` from this repository (either clone it or download the raw file).

2. **Transfer the file to your Android device**
   - Copy `index.html` to a memorable location on your device's storage (e.g. `Downloads/deep-web-research/index.html`).

3. **Open AI Edge Gallery**
   - Launch the **AI Edge Gallery** app on your Android device.

4. **Navigate to Skills**
   - Go to **Settings → Skills** (or the **Skills** tab, depending on your app version).

5. **Add a new skill**
   - Tap **"Add Skill"** or the **"+"** button.
   - When prompted, select **"Load from file"** and browse to the `index.html` file you transferred in step 2.

6. **Confirm the skill details**
   - The app will read the skill metadata from the file header:
     - **Name:** `deep-web-research`
     - **Description:** Research a topic using Wikipedia and DuckDuckGo…
   - Confirm to finish installation.

7. **Start chatting**
   - Select a Gemma model in the app and ask about any current event or factual topic. The model will invoke the skill automatically when it detects the query benefits from live web data.

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

- Android device with **AI Edge Gallery** installed
- Internet access on the device at query time
- No API keys or accounts needed
