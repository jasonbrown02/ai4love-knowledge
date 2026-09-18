# AI4Love System Specification
Version 3.3
Last updated: June 22, 2026
Purpose: Authoritative technical reference for all LLM sessions and collaborators

## Changelog from v3.2
- Frontend corrected from Next.js to the live React + Vite single-page application.
- Agent terminology clarified: seven core analysis agents plus Queue Cleanup and two resurrection workflows.
- MCP inventory corrected to 42 authenticated tools, including two narrowly gated write operations.
- API section relabeled as core dashboard endpoints and expanded to acknowledge supporting route groups.
- Cache policy corrected to private, no-store for authenticated API responses.
- Organization scoping clarified as authentication-derived, with authorized org switching for permitted roles.
- Completed Multer 2 migration removed from next priorities.
- CI gap documented: MCP tests and frontend production build are not currently exercised by CI.

## Companion Document
For product positioning, costs, onboarding detail, client personas, and LLM reasoning patterns, see AI4Love-Product-Overview.md. This spec covers technical architecture, data model, agents, API, and queue system.

## 1. What AI4Love Is

AI4Love is a for-profit relationship intelligence platform serving nonprofit organizations.

AI4Love connects to an organization's existing systems of record and generates actionable relationship insights. It does not replace CRMs, donation processors, email platforms, or volunteer tools.

AI4Love operates as an intelligence layer. The product is insight. Data orchestration is infrastructure.

### Positioning
- Customer: Nonprofit organizations (foundations, charities, development teams)
- Product type: Intelligence layer
- System of record: External platforms
- Action model: Human decision making, not automated outreach
- Target: organizations with 1,000 to 15,000 supporters

### Core Philosophy
1% Can. Small, consistent acts of care create durable change.

### Zero Custody Principle
Supporter data remains in each organization's primary systems of record wherever possible. AI4Love minimizes duplication and avoids functioning as a primary database of record. AI4Love stores only normalized activity data needed for intelligence.

## 2. System Architecture

Architecture Pattern: Hub and Spoke Intelligence Layer

### Spokes
- CRM systems
- Donation processors
- Email platforms
- Volunteer management tools
- Event platforms

### Integration Layer
- Make.com scenarios per organization
- Nango OAuth gateway (credentials owned by organization)
- Data normalization into canonical schema

### Hub
- Airtable base per organization (Business tier, 125K records per base)
- Unified activity stream centered on Participation

### Intelligence Layer
- Anthropic Claude API (Sonnet 4)
- Nine specialized agents
- Pinecone vector database (KindMind research index plus per-client vault)
- OpenAI embeddings (text-embedding-3-large)

### Application Layer
- React + Vite single-page dashboard on Vercel Pro (3 projects: frontend, backend, MCP)
- Serverless API routes
- MCP server for conversational access (42 authenticated tools)

### Data Flow

Source Systems
→ Nango OAuth
→ Make.com
→ Airtable (Participation table)
→ Make agents (nightly)
→ Claude API
→ Insights table
→ API routes
→ Dashboard UI

## 3. Three-Layer Model

### Layer 1: Deterministic Analysis (rule-based)
Nine nightly agents via Make.com apply fixed math: RFM scoring, rolling averages, decay functions, threshold triggers. This is not AI. It is rollups, formulas, and conditional logic.

### Layer 2: Text Generation (LLM-constrained)
Claude API writes human-readable insight text after Layer 1 pattern detection. The LLM receives only:
- Supporter name
- Detected pattern type
- Relevant metrics
- Full pre-fetched timeline

The LLM cannot access full records, trigger actions, or override suppression rules. Content Integrity Policy (v2026-04-07) is enforced on all prompts. Post-generation verification cross-checks AI-claimed metrics against actual Airtable data. Dashboard action generators (campaigns, messages, thank-yous, re-engagement) run server-side validateActionData() to strip invented supporters and correct hallucinated counts before output reaches frontend or Airtable.

### Layer 3: Human Action
Staff review dashboard insights and decide whether to act. No automated outreach. No loop closure.

Core philosophy: Suppression over speculation. Silence is safer than noise.

## 4. Design Principles

1. People is the root entity. Every insight belongs to a person.
2. Participation is the unified activity stream.
3. participated_at drives time analysis. Never use created_at.
4. Insights attach to People, not Participation.
5. No AI fields in source tables.
6. Identity flows through link fields only.
7. All metrics derive from formulas or rollups.
8. agent_queue_status lives on Participation (moved from People Feb 2026).
9. Health buckets derive from days_since_last_activity, not Airtable status.
10. Nurture handles groups. Connect handles individuals.

## 5. Core Data Model

### People
Root identity table. Unique by email. Contains demographic fields and rollups.

### Participation
Canonical activity stream. Every donation, volunteer act, or engagement maps here. Primary analytic date: participated_at. Hosts agent_queue_status field for nightly agent eligibility filtering.

### Donors
Raw donation records. Source table only.

### Volunteers
Raw volunteer records. Source table only.

### Engagements
Campaign and interaction records. Source table only.

### Events
Optional structured activity grouping.

### Insights
All AI outputs. One insight record per pattern per person.

No source table contains AI-generated fields.

## 6. Supporter Status Thresholds

Derived from days_since_last_activity across the full Participation stream.

- Active: 0 to 90 days
- Steady: 91 to 180 days
- Cooling: 181 to 365 days
- At-Risk: 366 to 730 days
- Lapsed: 731 days or more

## 7. Core Agents and Scheduled Workflows

Seven core analysis agents run nightly through Make.com. Three additional scheduled workflows handle queue cleanup and two resurrection cohorts. The operational workflows are documented separately from the seven core agents so product-facing agent counts remain unambiguous.

Each core analysis agent:
- Queries Airtable for eligible supporters
- Applies deterministic pattern detection and suppression gates
- Sends structured supporter payload to Claude
- Receives structured JSON
- Writes to Insights table
- Skips record if response is NO_INSIGHT

Agents 1 through 7 are the core intelligence agents. Workflow 8 is operational housekeeping. Workflows 9 and 9b surface deeply-lapsed resurrection candidates.

### Agent 1: At Risk Detection
Question: Who is drifting away?
Output: Risk factors, urgency window, reconnection strategy.

### Agent 2: Conversion Opportunities
Question: Who is ready for deeper engagement?
Output: Natural next step, effort level, timing, confidence.

### Agent 3: Recognition Triggers
Question: Who deserves celebration?
Output: Milestone narrative, channel recommendation, draft message.

### Agent 4: Campaign Intelligence
Question: What individual campaign patterns matter?
Rule: Individual level only. No segment analysis. Segment-level work happens in the Nurture dashboard.

### Agent 5: Relationship Deepening
Question: Who needs a human touch?
Rule: ask_allowed is always false. Pure connection, no ask attached.

### Agent 6: Cross-Agent Intelligence
Question: What does multi-agent overlap reveal?
Handles precedence conflicts. Catches situations like Agent 4 flagging campaign fatigue on a supporter Agent 2 is pushing toward conversion.

### Agent 7: KindMind Enrichment
Question: What does sector research recommend?
Enriches insight using Pinecone vector database (curated nonprofit sector research).

### Workflow 8: Queue Cleanup
Question: Did any supporters get missed?
Operational housekeeping. Reads from Participation only, runs at 04:00 to avoid conflict with Agent 9b.

### Workflow 9: Lapsed Donor Resurrection
Question: Who hasn't given in 5+ years but should be called?
Cohort: silent 5+ years, $500+ lifetime giving. Six detection patterns. Tiered cap structure (100 total per nightly run: 20 high, 40 medium, 40 low confidence). 90-day rotation. Action-driven removal.

### Workflow 9b: Recurring Pause Resurrection
Question: Whose monthly giving paused, is it worth a personal nudge?
Cohort: 1+ year since last donation, proven recurring history (3+ monthly gifts), $200+ lifetime. Five detection patterns. Focus on re-establishing the habit.

## 8. Agent Queue System

### Trigger Source
New Participation record.

### Process
1. Airtable automation sets agent_queue_status to Queued on Participation.
2. Make agents filter Queued records.
3. Agents process supporter.
4. Insights written.
5. Status reset to Processed.

Delta mode (incremental): Participation records flagged Queued only.
Full mode: reprocesses all supporters using defined eligibility filters.

People table has a rollup field using ARRAYUNIQUE(values) to surface queue status for Make.com views.

## 9. Dashboard Application

Four Pages. Each answers one question.

### Pulse
Question: What is happening now?
Displays raw momentum metrics. No AI narrative interpretation.

### Insights
Question: What patterns matter?
Aggregates all agent outputs. Includes cross-agent alerts.

### Nurture
Question: How healthy are supporter groups?
Segment health dashboard. Donors, Volunteers, Engaged Supporters. Health spectrum: Thriving, Steady, Cooling, At-Risk, Lapsed.

### Connect
Question: Who needs a personal touch?
Individual level actions only. Three sub-views: Celebrate (recognition), Reconnect (deeper conversation), Appreciate (gratitude with no ask).

### Cross Page Rules
- Dark theme
- Color system aligned to risk levels
- AI summary bar on every page
- Deduplication within sections only

The Loop (separate approval queue) is cancelled. Dashboard plus MCP connection covers all use cases.

## 10. Core Dashboard API Endpoints

/api/pulse
Returns at-risk counts and trend data.

/api/dashboard-insights
Returns all insights.

/api/nurture
Returns group health metrics and fatigue alerts.

/api/connect
Returns individual recognition and relationship opportunities.

All endpoints:
- Filter by organization
- Include CORS headers
- Return authenticated data with private, no-store cache policy
- Return proper HTTP status codes

The backend also exposes supporting route groups for authentication, Airtable access, integrations, uploads, research, exports, system operations, scheduled jobs, and administration. The four endpoints above are the core dashboard contract, not the complete backend API inventory.

## 11. Integration Model

AI4Love is an intelligence layer, not a system of record.

OAuth and vendor API connections are owned per organization. Nango acts as the OAuth gateway. Clients connect their platforms via the dashboard Integrations page and Nango stores credentials. Make.com pulls credentials from Nango when running syncs. AI4Love never handles vendor credentials directly.

AI4Love stores:
- Normalized activity data in Airtable
- Insight outputs
- Integration health metadata

AI4Love does not store:
- Vendor refresh tokens in Airtable
- Raw CRM full database exports beyond required activity data
- Credentials in dashboard code

Each organization has:
- Separate Airtable base
- Separate Make scenario set
- Shared dashboard codebase
- Organization scoping derived from the authenticated user; authorized admin flows may select an organization explicitly

## 12. Action Model

AI4Love surfaces recommendations.

Staff take action manually.

No automated sending out of the box.
No automatic campaign triggers.
No automated fundraising flows.

Outbound messaging to supporters may be enabled per client in future implementations, subject to contractual agreement and explicit client opt-in. It is not part of the core product.

## 13. MCP Server

Provides conversational access to supporter and insight data.

Enables staff to query intelligence through Claude without logging into dashboard.

Currently at v1.1.0. Authenticated clients receive 42 tools: diagnostic, query, operational, and visual scene tools. Forty are read-only in behavior. Two are narrowly gated writes: add_to_kindmind writes curated research to Pinecone for allowlisted curator organizations, and mark_campaign_refined updates an organization-scoped Generated Campaigns record. Supporter and source-system records are not writable through MCP.

Unauthenticated clients receive diagnostic tools only. Data tools require OAuth or a provisioned organization API key. Authentication failures are returned as MCP-level tool errors so connector sessions remain stable.

Pattern: mcp.ai4love.ca/[org-slug]
Reference deployment: stilltide-mcp.vercel.app

Second access path alongside dashboard.

## 14. Tool Stack

### Infrastructure
- Vercel Pro (3 projects: frontend, backend, MCP)
- Airtable Business (per-org bases at 125K records each)
- Anthropic Claude API (Sonnet 4)
- OpenAI API (text-embedding-3-large for KindMind)
- Pinecone (vector DB)
- Nango (OAuth gateway)
- Clerk (passwordless auth, SOC 2 Type II)
- Doppler (secrets management, single source of truth, syncs to Vercel)
- Resend (transactional email)

### Development
- Windsurf Pro (UI work)
- Claude Max (planning, repo execution)
- Claude Code / CLI (system changes, deployments)
- ChatGPT Plus (synthesis, writing)
- Gemini Pro (sanity check)

### Communication
- Zoho Workplace (jason@ai4love.ca, info@ai4love.ca)

### Research
- Perplexity Pro (free until October 2026)

## 15. Cost Model

Per client at 5,000 supporters:

- Anthropic Claude API (Sonnet 4): ~$200/mo
- Make.com (~150K ops): ~$137/mo
- Airtable Business: ~$45/mo
- OpenAI API (embeddings): ~$3/mo
- Pinecone: $0 to $35/mo
- Vercel Pro (amortized): ~$20/mo
- Total COGS: ~$405 to $440/mo

Claude cost scales by:
supporter_count × average_token_payload × agents × frequency

Agents must filter aggressively before LLM call. Pattern detection is deterministic and pre-filtered.

Target margin at Core pricing ($1,800/mo): ~77%.

## 16. Scalability and Airtable Limits

Practical operating ceiling per organization:
- 20,000 People
- 100,000 Participation records
- 7 core nightly analysis agents scanning eligible supporters, plus 3 scheduled operational/resurrection workflows

Beyond this:
- Rollups slow
- Automations queue
- Agent runtime increases
- API throughput degrades

Mitigation:
- Archive historical Participation outside analytic window
- Precompute rollups
- Restrict nightly eligibility cohorts
- Monitor runtime

Migration trigger threshold:
- Participation greater than 250,000
- Or nightly agent runtime greater than 2 hours

Migration path:
- Replace Airtable with scalable database
- Retain canonical schema
- Retain agent logic
- Retain dashboard

## 17. Failure Modes

AI4Love anticipates:
- Integration sync failure
- Partial Participation backfill
- Agent queue stall
- Pinecone enrichment failure
- Empty Client Vault
- Low confidence suppression
- Claude API 529 errors (retry logic implemented across all agents)

System suppresses insight rather than guessing. Silence is preferred over incorrect output.

## 18. Operational Status

### Operational
- Seven core analysis agents running nightly
- Queue Cleanup plus two resurrection workflows scheduled separately
- Live dashboard
- MCP server active (v1.1.0)
- KindMind enrichment live
- Agent queue system active
- Content Integrity Policy enforced (v2026-04-07)
- Post-generation verification active

### Next Priorities
- IT security one-pager PDF for partner onboarding
- API key rotation automation (Airtable, Make.com, Vercel)
- Make.com ingestion scenarios for Mailchimp, Environics, Blackbaud
- Converge Pinecone dependency versions across backend and MCP
- Add MCP tests and frontend production build verification to CI
- Verify any externally configured MCP rate limits before publishing fixed limits in customer-facing materials

## 19. LLM Session Boot Block

Use this framing when starting a new LLM session:

AI4Love is a relationship intelligence platform for nonprofit organizations. It integrates external systems into a unified Participation model in Airtable. Seven core agents analyze supporter data and write structured insights nightly. Separate scheduled workflows clean the queue and surface two resurrection cohorts. The dashboard and MCP server surface intelligence. Staff act manually. AI4Love is an intelligence layer, not a CRM. It does not automate supporter outreach.

Then define the specific task.
