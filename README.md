# Ledger Briefing — Binance Agent OS + Dune

A Claude skill that explains **why** a crypto asset is moving, not just what price it's at — by combining live Binance market data with on-chain event data from Dune, and synthesizing both into a plain-English briefing for people who aren't professional traders.

Built for the Binance Agent OS Mini Hackathon (Track B — Connect & Trade), combining Binance Agent OS with a Dune MCP connection.

## Why

Binance Agent OS gives an AI agent the market's price action. That's the *effect*. On-chain data — exchange flows, stablecoin mints, whale transfers — is the *cause*. Most people only ever see the effect: a red or green number with no context. This skill sits between the two data sources and gives a normal investor an honest, jargon-free answer to "should I actually care about this?"

## Installation

1. Download or clone this repo
2. Zip the `ledger-briefing` folder (folder itself as the root of the zip)
3. In Claude.ai, go to Settings, then Customize, then Skills
4. Click the plus button, then "Create skill", then "Upload a skill"
5. Upload the zip file, then toggle the skill on
6. Connect Binance Agent OS and Dune under your MCP connectors

See `SKILL.md` for the full workflow logic, and the `references/` folder for the confidence/magnitude thresholds and exact output structure.

## Example

Prompt: *"Why is BNB down today?"*

Result:

> BNB is down 4% today, which coincides with a large wallet moving $12M to an exchange deposit address about 40 minutes ago — a pattern that's historically meant short-term selling pressure rather than a fundamental shift.
>
> **Market pulse:** $612.40, -4.1% (24h), sell-side order book pressure is heavier than usual
> **On-chain signal:** large exchange inflow — medium magnitude
> **Historically:** inflows like this have often preceded further short-term selling, though not always
> **Confidence:** medium — timing lines up but no second confirming signal yet
>
> This is market and on-chain information, not financial advice — always do your own research before making a decision.

## What this is not

Not a trading bot. It never recommends buying, selling, or holding — it only explains context. Any trade decisions stay entirely with the user.

## License

MIT — free to use, modify, and share.
