# The Agents

v2 Insights Engine, rebuilt April 2026. Ten agents now in production. Each runs nightly via Make.com on a staggered schedule.

## The full list

| # | Agent | Purpose | Schedule (UTC) | Question it answers |
|---|---|---|---|---|
| 1 | At-Risk Detection | Protect relationships | 02:00 | Who's drifting away? |
| 2 | Conversion Opportunities | Grow support | 02:15 | Who's ready for more? |
| 3 | Recognition Triggers | Celebrate achievements | 02:30 | Who deserves recognition? |
| 4 | Campaign Intelligence | Inform strategy | 02:45 | What's working? |
| 5 | Relationship Deepening | Build connection | 03:00 | Who needs a human touch? |
| 6 | Cross-Agent Intelligence | Surface hidden patterns | 03:15 | What do we see across all agents? |
| 7 | KindMind Enrichment | Ground in sector research | 03:30 | What do best practices say? |
| 8 | Queue Cleanup | Catch missed records | 04:00 | Did any supporters get missed? |
| 9 | Lapsed Donor Resurrection | Win back deeply-lapsed donors | 03:45 | Who hasn't given in 5+ years but should be called? |
| 9b | Recurring Pause Resurrection | Re-establish broken monthly habits | 04:00 | Whose monthly giving paused — is it worth a personal nudge? |

## v2 architecture (April 2026)

- **Agents 1-5** use the prefetch proxy pattern. Make.com pulls the queue, the backend pre-fetches full supporter timelines from Airtable, then sends everything to Claude in one call. No MCP at generation time.
- **Agent 6** uses the direct proxy. Reads today's insights from Agents 1-5, sends them to Claude for cross-agent pattern detection, writes results server-side.
- **Agent 7** uses Pinecone + Claude. Embeds each insight, finds related sector research, generates practical guidance.
- All agents run on **claude-sonnet-4-6**.
- All agents are guardrailed by the **Content Integrity Policy (v2026-04-07)** which prohibits fabrication of any facts not present in provided data.
- **Archived insights are filtered** from all surfaces: MCP tools, dashboard queries, agent inputs.
- **Cost logging** writes per-run token counts and USD cost to the Engine Logs table.
- **Insight verification** (Agents 1-6) compares claimed metrics against actual Airtable data after each write.

## The difference between Agent 5 and the others

| Agents 1-4 | Agent 5 |
|---|---|
| "Save this revenue" | "Check if they're okay" |
| "Convert this volunteer" | "Thank this volunteer" |
| "Celebrate their milestone" | "Celebrate your time together" |
| "Optimize timing" | "Just connect" |

This is the "Love" in AI4Love.

## Agent 6 as orchestration

When Agent 4 flags campaign fatigue on the same supporter Agent 2 is pushing a conversion ask toward, Agent 6 catches it and applies precedence rules:

- Fatigue suppresses all asks
- Recognition before re-engagement
- Relationship before conversion

The system argues with itself so staff don't have to.

## v1 → v2 history

v1 (pre-April 2026) used pre-aggregated rollup data sent to Claude. v2 uses live timeline data pre-fetched per supporter. v1 insights (897 total, ~67% hallucination rate) were archived on April 10, 2026. v2 insights run at ~0% hallucination rate with content integrity policy enforced.

## Source of truth

Notion: Agent Personas page (https://www.notion.so/2f6133829a6b80d89be9dfe3059f5134)
System Spec: v3.2 (May 12, 2026), section 7.

**Note on the count:** System Spec v3.2 says "Nine Agents" because it treats Agent 9b as a sub-variant of Agent 9 (both surface deeply-lapsed resurrection candidates). The Notion Agent Personas page lists them as separate operational units with distinct schedules and detection patterns. Both views are correct; the knowledge base mirrors Notion (ten files) since they run as ten distinct Make.com scenarios.

Each agent has its own Notion subpage with full spec. Files in this folder are stubs to be populated as needed.

## Per-agent Notion links

- [Agent 1: At-Risk Detection](https://www.notion.so/2f6133829a6b80c2bfb0eb3f269bcb68)
- [Agent 2: Conversion Opportunities](https://www.notion.so/2f6133829a6b811c8f1ffec8de20e012)
- [Agent 3: Recognition Triggers](https://www.notion.so/2f6133829a6b817e9e8ec506675ff606)
- [Agent 4: Campaign Intelligence](https://www.notion.so/2f6133829a6b81c79a7ace971cebe0d4)
- [Agent 5: Relationship Deepening](https://www.notion.so/2f6133829a6b811f806af13f56ee656f)
- [Agent 6: Cross-Agent Intelligence](https://www.notion.so/2f7133829a6b81688f99f63b09f3d85e)
- [Agent 7: KindMind Enrichment](https://www.notion.so/2f9133829a6b812aa1d1f411fddd9c59)
- [Agent 8: Queue Cleanup](https://www.notion.so/359133829a6b812d96ccc72ea71c5e49)
- [Agent 9: Lapsed Donor Resurrection](https://www.notion.so/359133829a6b8138be82db7d2d5a6188)
- [Agent 9b: Recurring Pause Resurrection](https://www.notion.so/359133829a6b81feb1e3eb699bebe474)
