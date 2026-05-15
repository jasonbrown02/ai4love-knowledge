# Cost Model

Per-client unit economics. Source: System Spec v3.2 section 15.

## COGS at 5,000 supporters per client

| Component | Monthly cost |
|---|---|
| Anthropic Claude API (Sonnet 4) | ~$200 |
| Make.com (~150K ops) | ~$137 |
| Airtable Business | ~$45 |
| OpenAI API (embeddings for KindMind) | ~$3 |
| Pinecone | $0 to $35 |
| Vercel Pro (amortized) | ~$20 |
| **Total** | **~$405 to $440** |

## Margin

Target margin at Core pricing ($1,800/mo): ~77%.

## Claude cost scaling formula

```
supporter_count × average_token_payload × agents × frequency
```

Implication: agents must filter aggressively before LLM call. Pattern detection runs deterministically and pre-filters before any token is sent to Claude.

This is one of the key reasons for the three-layer model (deterministic analysis → LLM text generation → human action). Layer 1 cuts cost by orders of magnitude before Layer 2 runs.

## Infrastructure baseline (not per-client)

Running infrastructure cost across all clients: ~$780/month.

First client (JBHF pilot) is a conscious strategic investment in proof-of-concept. Margin improves with each additional client added against the same infrastructure baseline.

## What this means for pricing strategy

- Core tier at $1,800/mo lands at ~77% gross margin per client. Healthy for a managed-intelligence service.
- Backfill at onboarding (~$420 USD for 6,000 supporters historical data) is one-time, not recurring.
- Cost grows with supporter count, not feature count. Adding agents has marginal incremental cost because all agents share the deterministic Layer 1 filter.

## Source

System Spec v3.2 section 15.
