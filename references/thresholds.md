# Thresholds — Magnitude & Confidence

These are starting heuristics, not hard rules. Adjust for the specific asset's typical volume (a $2M transfer is huge for a low-cap token and trivial for BTC).

## Magnitude (size of the on-chain event, relative to the asset)

| Magnitude | Exchange flow | Stablecoin mint/burn | Wallet transfer |
|---|---|---|---|
| Low | < 0.5% of 24h volume | < $50M | < $1M, or normal for a known active wallet |
| Medium | 0.5–2% of 24h volume | $50M–$300M | $1M–$10M from a wallet with no clear labeled pattern |
| High | > 2% of 24h volume | > $300M | > $10M, or from a wallet previously tied to a large exchange/fund |

## Confidence (how sure we are the on-chain event actually explains the price move)

- **High** — the event's timing lines up closely (within a few hours) with the price move, the magnitude is meaningful relative to normal activity for that asset, and there isn't an obvious competing explanation (e.g. a scheduled macro news event at the same time).
- **Medium** — timing is plausible but not tight, or the event is real but modest in size relative to the move, or there's a plausible competing explanation we can't rule out.
- **Low** — we found *something* on-chain but it's small, old, or its relationship to the price move is speculative. Also use Low whenever no on-chain driver was found at all — pair it with an honest "may just be normal volatility" framing rather than forcing a false narrative.

## Tool-call budget

Don't chase a perfect answer at the cost of a slow or bloated response:
- 1 discovery/search query to find the right table or metric for the asset
- 1 focused query against that table
- If neither turns up anything relevant, stop and report "no clear on-chain driver" rather than continuing to dig — that's a legitimate, honest outcome, not a failure.
