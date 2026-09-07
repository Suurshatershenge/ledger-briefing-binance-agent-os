# Output Format

Structure every briefing in this order. Keep it conversational — this is not a template to fill in mechanically with headers, it's a shape to write naturally within.

## 1. The headline (one sentence)

Directly answers "why is this moving." Plain English, no jargon, states the connection between market and on-chain data — or honestly states there isn't one.

> "BNB is down 4% today, which coincides with a large wallet moving $12M to an exchange deposit address about 40 minutes ago — a pattern that's historically meant short-term selling pressure rather than a fundamental shift."

> "ETH is up slightly today, but there's no clear on-chain driver behind it right now — this looks like normal day-to-day movement."

## 2. Market pulse (brief)

Current price, 24h change, and a one-line read on order-book pressure ("buy-side is heavier right now" / "roughly balanced"). Numbers only — no interpretation yet, that happens in the headline and historical note.

## 3. On-chain signal (brief)

Name the event plainly (or state that none was found), and its magnitude (low/medium/high per `thresholds.md`).

## 4. Historical note (one cautious sentence)

What this *kind* of pattern has tended to mean before — phrased as a tendency, never a prediction or instruction.

> "Large pre-drop exchange inflows like this have often preceded further short-term selling, though not always."

Avoid: "this means it will keep dropping" — that crosses into advice/prediction.

## 5. Confidence

State low/medium/high per `thresholds.md`, briefly explain why in one clause if it's not obvious.

## 6. Optional: the raw numbers

Only if the user wants the underlying evidence (they ask, or you're providing a "show technical details" aside). Include actual figures, table/metric names from Dune, and the exact market data pulled.

## Deep-dive additions

When the user asked for a fuller read (see `SKILL.md`'s deep-dive trigger), add two things:

**Leverage/hype read** — one or two sentences on what funding rate + open interest + large trades suggest about how much of the current move is speculation vs. real flow. Example:

> "Funding is sharply positive and open interest has climbed alongside price — a good chunk of this move looks like leveraged longs piling in, not necessarily new capital."

**The chart** — present the single generated chart right after the on-chain signal section, with one sentence on what it shows. Don't caption it with more than that; let the chart do the work.

**Close the loop explicitly** — the deep-dive's final synthesis sentence, right before the guardrail line, should directly answer "is this hype or is this real": state plainly whether market sentiment and on-chain reality are pointing the same direction, or diverging.

## 7. Guardrail line (always, every time)

One short sentence, varied in wording but consistent in meaning:

> "This is market and on-chain information, not financial advice — always do your own research before making a decision."

## What never to do

- Never phrase anything as "you should buy/sell/hold."
- Never state a causal on-chain link with certainty if confidence is Low.
- Never fabricate a specific dollar figure, wallet address, or table name if the Dune query didn't actually return one.
- Never bury the headline under raw data — lead with the plain-English sentence.
