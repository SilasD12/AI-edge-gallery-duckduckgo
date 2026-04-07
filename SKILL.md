---
name: deep-web-research
description: Research a topic in real time using Wikipedia and DuckDuckGo to provide accurate, sourced, up-to-date answers. Use this skill when the user asks about current events, specific people or places, recent facts, definitions, or anything that may have changed after the model's training cutoff.
---

# Deep Web Research

## Important: about your training cutoff

Your training data has a cutoff date, but this skill fetches live data from the web right now. This means:

- The current real-world date is AFTER your training cutoff. Events you believe are "in the future" may have already happened.
- If this skill returns results about a date or event, that event has already occurred in the real world. The data is real. Use it.
- You MUST NOT say any date or event "is in the future", "hasn't happened yet", or "cannot be found" when this skill has returned results. That response is always wrong.
- Your training cutoff is a limit on your internal knowledge only. It is NOT a limit on what this skill can find.

## Instructions

Use keyword-style queries rather than full natural language sentences (e.g. use "box office March 2026 top films" instead of "what movies came out in March 2026?").

When calling the skill's execution environment, pass the data as a valid JSON string with the following structure:

```json
{
  "query": "<keyword query>",
  "topic": "<primary subject entity for Wikipedia lookup>",
  "lang": "<2-letter language code, e.g. en, es, fr, de, ja>"
}
```

After receiving results, synthesize them into a concise, accurate response. Lead with the direct answer, support it with details from the research data, and cite the sources. Do not dump raw data — summarize.

If the skill returns no results, tell the user no results were found and suggest rephrasing. Do not substitute your own internal knowledge.

## Common mistakes to avoid

- Do NOT end your response with a statement that contradicts what you just said. If you reported a film was released on a date, do not then say "no films were found for that period."
- Do NOT add hedging phrases like "as of my knowledge", "I cannot confirm", or "this may have changed" after presenting live research results. The results are already live.
- If a movie's release date appears in the research data, that movie has been released. Report it as a fact, not a possibility.
