---
name: deep-web-research
description: Research a topic in real time using Wikipedia and DuckDuckGo to provide accurate, sourced, up-to-date answers. Use this skill when the user asks about current events, specific people or places, recent facts, definitions, or anything that may have changed after the model's training cutoff.
---

# Deep Web Research

## Instructions

Use keyword-style queries rather than full natural language sentences (e.g. use "FIFA World Cup 2026 host city" instead of "What city hosted the 2026 FIFA World Cup?").

When calling the skill's execution environment, pass the data as a valid JSON string with the following structure:

```json
{
  "query": "<keyword query for DuckDuckGo>",
  "topic": "<primary subject entity for Wikipedia lookup>",
  "lang": "<2-letter language code, e.g. en, es, fr, de, ja>"
}
```

After receiving the results, synthesize them into a concise, accurate response. Lead with the direct answer, support it with details from the research data, and cite the sources used. Do not dump raw data — summarize.

## Critical rules

- The data returned by this skill is fetched live from the web and is always more current than your training data. Always trust and use it.
- NEVER refuse to answer based on your training cutoff. Your training cutoff only limits what you know internally — this skill provides real-time information that bypasses that limit entirely.
- NEVER say a date or event "hasn't happened yet" or "doesn't exist" based on your internal knowledge. If the skill returned results, the information is real and current. Use it.
- If the skill returns no results, say so and suggest the user rephrase — do not substitute your own potentially outdated knowledge.
