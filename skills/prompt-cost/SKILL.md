---
name: prompt-cost
description: "Render the token usage and dollar cost of a prompt from the current Claude Code session as a self-contained HTML report for live demos. Use this skill whenever the user says 'show the cost of that prompt', 'how much did that prompt cost', 'prompt cost', '/prompt-cost', or wants a visual on-screen cost breakdown of a recent turn. Output is a single self-contained `.html` file with a clean, professional design showing input/output token counts, pricing, and cost calculations."
---

# Prompt Cost Report

Render token usage and pricing data as a clean, professional HTML report. Output is a single self-contained `.html` file.

The report should be clear and scannable — designed for live demos and quick cost reviews. Include model information, token counts (input and output), pricing per token, and total cost. Avoid clutter; let the numbers speak.

## How to use this skill

1. **Read `references/template.html` first.** It is the canonical source for every color, font, and component class. Copy tokens and component markup directly — do not reconstruct them from memory. The template includes a masthead, key figures row, and detailed cost breakdown table.
2. Gather the token usage data from the Claude Code session (input tokens, output tokens, model used).
3. Calculate costs using the pricing data for the specific model (available in Claude API documentation).
4. Save the result to an artifact or output location and deliver it to the user.
5. Keep everything in one file — no external dependencies required.

## Report structure

Every prompt-cost report includes:

- **Masthead** — eyebrow labeling it as a "Prompt Cost Report," model name and ID, and the date/time of the turn.
- **Key figures** — a ruled `.figures` row showing: total cost (in USD), input tokens, output tokens, and total tokens. Lead with the most visually important metric (total cost).
- **Pricing details** — a `.data` table with rows for: model name, input token price, output token price, input tokens used, input cost, output tokens used, output cost, and total cost. Keep prices in scientific notation or ¢ per 1K tokens for clarity.
- **Summary note** — one short sentence explaining what was analyzed (e.g., "Cost for the turn processing your request to generate a dashboard").
- **Colophon** — always close with provenance: Claude model ID, token counts source (Claude Code session), pricing source (Claude API pricing as of [date]), and "Built with Claude Code."

## Design and voice

- **Typography** — consistent with academic-dashboard: serif for titles, monospace for prices and numbers.
- **Color** — use a neutral palette. Highlight the total cost prominently (e.g., in a slightly darker shade or with subtle background). Use muted tones for supporting data.
- **Numbers** — prices should be formatted clearly (USD, with $ prefix and cents, or in fractions of ¢ per 1K tokens). Token counts should use comma separators for readability (e.g., "10,000" not "10000").
- **Voice** — factual and direct. No hype. Let the cost data stand on its own.

## Output

Save to an artifact and deliver to the user. Keep it self-contained so it can be opened directly in a browser or shared as a standalone file.
