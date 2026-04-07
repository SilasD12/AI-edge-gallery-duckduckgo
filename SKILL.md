---
name: deep-web-research
description: Research a topic using Wikipedia and DuckDuckGo to provide accurate, sourced, up-to-date answers when the model's training data may be insufficient.
---

# Deep Web Research

## When to invoke this skill

Use this skill when the user asks about:
- Current events, recent facts, or time-sensitive information
- Specific people, places, organizations, or historical events
- Definitions, statistics, or data where accuracy matters
- Anything that may have changed after the model's training cutoff

Do NOT use this skill for:
- Personal advice, opinions, or creative writing tasks
- Math, coding, or logic problems
- Casual conversation

## Instructions

Call the `run_js` tool with the following exact parameters:
- script name: index.html
- data: A JSON string with the following fields:
  - query: String. The full, specific search query from the user's message. Be precise — include context (e.g., "2026 FIFA World Cup host city" not just "host city").
  - topic: String. The primary subject entity for the Wikipedia lookup. Extract ONLY the core noun subject — strip action words like "who is", "what is", "when did", "how many" (e.g., use "FIFA World Cup 2026" not "who won the 2026 FIFA World Cup").
  - lang: String. 2-letter language code matching the user's language (e.g., "en", "es", "fr", "de", "ja", "ko", "zh", "pt", "ar", "hi").

## After receiving results

Synthesize the research data into a clear, accurate response:
1. Lead with the direct answer to the user's question
2. Support it with relevant details from the research data
3. Cite sources inline (e.g., "According to Wikipedia...")
4. If the data is insufficient or ambiguous, say so and suggest the user verify via a browser
5. Keep your response concise — summarize, do not dump raw data
