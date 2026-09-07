---
name: ledger-briefing
description: A Claude skill built on Binance Agent OS and a Dune MCP connection that explains WHY a crypto asset is moving, not just what price it's at. Combines live Binance market data (price, 24h change, order-book depth) with on-chain event data from Dune (exchange flows, stablecoin mint/burn, large wallet transfers, DEX activity) into a single plain-English briefing for people who are not professional traders. Use this skill whenever the user asks things like "why is BTC down today," "should I be worried about this dip," "what's happening with ETH," "explain this price move," or generally wants to understand a market move rather than just see a number. Also trigger when the user explicitly asks for a "market briefing," "on-chain explanation," or to combine market data with on-chain data for an asset.
---

# Ledger Briefing

Binance Agent OS shows *what* the market is doing. On-chain data shows *why* it's about to, or just did. This skill's job is to sit between the two and answer one question in plain English: **"Should I actually care about this move?"**

Market data alone tends to reflect **hype and sentiment** — order flow, leverage, funding rates are all downstream of what traders *believe* is happening. On-chain data is closer to **what's actually happening** — real capital moving, real supply changes. The core value of this skill is triangulating between the two: when they agree, confidence goes up; when market sentiment is running hot but on-chain shows nothing backing it, that gap itself is the insight worth surfacing.

The audience is an everyday investor, not a trader. Never use unexplained jargon, never suggest a trade, and never present a coincidence as a certainty.

## Workflow

When a user asks about an asset's price movement, follow this sequence:

### 1. Get the market data (Binance Agent OS)

Two levels of depth, depending on what the user is asking for:

**Standard** — for a quick "why is X moving" question:
- Current price and 24h % change
- 24h high / low
- Order-book depth (bid vs. ask volume) to gauge short-term buy/sell pressure

**Deep dive** — when the user asks for a fuller read, a "state of the token," or explicitly wants to gauge hype/leverage vs. reality, also pull:
- **Recent large trades / tape** — outsized single trades reveal real order flow, not just resting book depth
- **Funding rate and open interest** (if a perpetual market exists for the asset) — this is the clearest read on how much *leverage and speculation* is baked into the current move. Sharply positive funding + rising open interest during a rally is a hype/leverage signal, not necessarily a fundamentals signal — flag this distinction explicitly to the user.

If Binance Agent OS is not connected, fall back to Binance's public REST endpoints (`/api/v3/ticker/24hr`, `/api/v3/depth`, `/api/v3/trades`, and `/fapi/v1/fundingRate` / `/fapi/v1/openInterest` for perps) — these require no authentication.

### 2. Investigate the on-chain cause (Dune)

Using the Dune MCP connection, look for genuinely relevant on-chain activity from the last 24–48 hours. In priority order, check for:
- **Exchange net inflow/outflow** — large wallet-to-exchange deposits (often precede sell pressure) or withdrawals (often precede accumulation narratives)
- **Stablecoin mint/burn activity** — large USDT/USDC mints are a classic "dry powder entering the market" signal
- **Unusually large wallet transfers** ("whale" movement)
- **DEX liquidity or volume shifts** — large swaps or pool changes that can lead CEX price discovery

Budget: a discovery query plus one focused query is normally enough. Don't burn excessive tool calls chasing a signal that isn't there — see `references/thresholds.md` for how much digging is proportionate.

**If nothing concrete turns up, say so.** A clean "no clear on-chain driver right now — this may just be normal volatility or a reaction to news" is a valid and honest answer. Never invent a number or manufacture a cause to seem more insightful.

**In deep-dive mode, generate one chart.** Once you've found the clearest on-chain signal (e.g. exchange net flow over the last 48h, or a stablecoin mint/burn timeline), use Dune's query + visualization tools to build a single chart of that specific metric rather than only describing it in text. One well-chosen chart beats a wall of numbers — don't generate more than one unless the user asks for it.

### 3. Synthesize — don't just report

Don't show two separate data dumps. Connect them into cause-and-effect language. See `references/output-format.md` for the exact structure and tone to use, and `references/thresholds.md` for how to assign magnitude and confidence levels consistently.

### 4. Always close with the guardrail line

Every briefing ends with a short, plain reminder that this is informational context, not financial advice, and that on-chain activity is a correlate, not a guarantee. Never phrase output as a buy/sell recommendation, even implicitly (e.g. avoid "this is a good entry point" or "you may want to sell").

## Tone rules

- Plain English by default. Numbers and specific on-chain terms belong in an optional "the raw numbers" aside, not the headline.
- One synthesized sentence should answer the user's actual question before anything else. Don't make them read a paragraph to find the point.
- Calibrate confidence honestly. A stablecoin mint of $500M is a very different signal strength than one mid-size wallet moving $2M — don't flatten these into the same tone of certainty.
