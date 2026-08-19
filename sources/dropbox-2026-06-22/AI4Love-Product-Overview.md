Changelog

Version 0.5
• Confirmed the dashboard stack as React + Vite
• Clarified seven core analysis agents versus three scheduled operational/resurrection workflows
• Updated MCP scope to 42 authenticated tools, including two narrowly gated writes
• Confirmed Clerk authentication, Doppler secrets management, and three Vercel projects

Version 0.4
• Standardized Seven Agents across document
• Clarified AI4Love as normalized shadow intelligence layer
• Defined deterministic pattern detection vs LLM narrative layer
• Marked agents fully operational
• Removed automated supporter outreach examples
• Added Airtable scalability ceilings and migration path
• Added intelligence cost modeling formula
• Reinforced Participation as analytic source of truth
• Clarified Campaign Agent vs Nurture boundary
• Added explicit failure modes section

⸻

For LLMs: How to Use This Document

Purpose
This is the source of truth for how AI assistants reason about AI4Love.

AI4Love is an intelligence layer for nonprofit organizations.
It integrates external systems into a unified Participation model in Airtable.
Seven core agents analyze supporter data nightly and write structured insights.
Separate workflows clean the queue and surface two resurrection cohorts.
The dashboard surfaces insights.
Staff act manually.

AI4Love does not automate supporter outreach.

⸻

Core Positioning

AI4Love is a relationship intelligence platform.

It connects to existing systems of record.
It normalizes activity data into a unified Participation model.
It analyzes behavioral patterns.
It surfaces structured insight records.

Primary systems of record remain external.

AI4Love maintains a normalized shadow dataset solely for intelligence and analytics.

It does not function as a transactional CRM.
It does not send supporter communications automatically.
All external-facing action is human-driven.

⸻

Philosophical Doctrine
	1.	People is the root entity.
	2.	Participation is the unified activity stream.
	3.	Participation is the analytic source of truth.
	4.	participated_at drives all time-based analysis.
	5.	Insights attach to People only.
	6.	No AI-generated fields exist in source tables.
	7.	Identity flows through link fields only.
	8.	Health buckets derive from recency, not static status.
	9.	AI4Love is intelligence, not automation.
	10.	Org isolation is absolute.

⸻

Core Data Model

People
Root identity table. Unique by email.

Participation
Canonical activity stream.
Every donation, volunteer act, or engagement maps here.
Primary analytic date: participated_at.

Donors
Raw donation records. Source table only.

Volunteers
Raw volunteer records. Source table only.

Engagements
Campaign and interaction records. Source table only.

Events
Optional grouping entity.

Insights
All AI outputs. One insight per pattern per person.

Participation replaces legacy cross-table analytics.
All dashboards and metrics derive from Participation.

⸻

Core Analysis Agents and Scheduled Workflows

Seven core analysis agents run nightly via Make.com.

They are fully operational.

Agent flow:
	1.	Query Airtable for eligible supporters
	2.	Apply deterministic pattern detection logic
	3.	Apply suppression gates
	4.	If eligible, send structured summary payload to Claude
	5.	Claude generates structured insight text only
	6.	Insight written to Insights table
	7.	If no pattern qualifies, no record created

The system detects patterns.
The LLM generates narrative text.

The LLM does not:

• Select supporters
• Score confidence
• Override suppression
• Choose actions
• Alter confidence values

⸻

Agent Roles
	1.	At Risk Detection
	2.	Conversion Opportunities
	3.	Recognition Triggers
	4.	Campaign Intelligence (individual-level only)
	5.	Relationship Deepening
	6.	Cross-Agent Intelligence
	7.	KindMind Enrichment

Scheduled operational and resurrection workflows:
	•	Queue Cleanup checks for missed Participation records.
	•	Lapsed Donor Resurrection surfaces deeply lapsed donors with strong re-engagement signals.
	•	Recurring Pause Resurrection surfaces proven recurring donors whose giving habit stopped.

These workflows are not included in the seven-agent product count.

Campaign Intelligence detects individual campaign pattern signals only.

Nurture dashboard handles segment-level campaign drafting.

They are separate layers.

⸻

No Automated Supporter Outreach

AI4Love does not automatically send:

• Emails
• SMS
• Campaign sequences
• Fundraising appeals

AI4Love surfaces recommendations only.
Staff act manually.

Internal sync automations are allowed.
External supporter automation is not part of core product.

Case-by-case enterprise implementations may differ contractually.

⸻

Dashboard Engines

Pulse
Raw momentum metrics derived from Participation.

Insights
All agent outputs aggregated.

Nurture
Segment health derived from Participation recency and activity volume.

Connect
Individual-level prioritization.

All analytics derive from Participation.
Do not use created_at for reporting.

⸻

Integration Architecture

Spokes
CRM systems
Donation processors
Email platforms
Volunteer tools
Event platforms

Integration Layer
Make.com per organization
OAuth owned by organization
Data normalized into Participation

Hub
Airtable base per organization

Intelligence Layer
Seven core analysis agents plus three scheduled operational/resurrection workflows
Claude API
Pinecone vector enrichment

Application Layer
React + Vite dashboard
Serverless API routes
MCP server with 42 authenticated tools; two narrowly gated writes do not modify supporter or source-system records

⸻

Scalability and Airtable Limits

Practical operating ceiling per organization (Airtable Business plan, 125K records/base):

• 15,000-20,000 People
• 75,000-100,000 Participation records
• 7 core nightly analysis agents scanning eligible supporters

Beyond this:

• Rollups slow
• Automations queue
• Agent runtime increases
• API throughput degrades

Mitigation:

• Archive historical Participation outside analytic window
• Precompute rollups
• Restrict nightly eligibility cohorts
• Monitor runtime

Migration trigger threshold:

Participation > 250,000
or nightly agent runtime > 2 hours

Migration path:

• Replace Airtable with scalable database
• Retain canonical schema
• Retain agent logic
• Retain dashboard

Architecture allows evolution.

⸻

Intelligence Cost Model

Claude cost scales by:

supporter_count × average_token_payload × agents × frequency

Agents must filter aggressively before LLM call.

Pattern detection is deterministic and pre-filtered.

⸻

Make.com Dependency

Each organization:

• Separate Airtable base
• Separate Make scenario set
• Separate OAuth credentials

Templating discipline required:

• Versioned scenario templates
• Naming conventions
• Field mapping standards

Make is current orchestration layer.
It is replaceable if scale demands.

⸻

Failure Modes

AI4Love anticipates:

• Integration sync failure
• Partial Participation backfill
• Agent queue stall
• Pinecone enrichment failure
• Empty Client Vault
• Low confidence suppression

System suppresses insight rather than guessing.

Silence is preferred over incorrect output.

⸻

Operational Status

Seven core analysis agents running nightly
Queue Cleanup and two resurrection workflows scheduled separately
Dashboard live
KindMind enrichment live
MCP active at v1.1.0
Org isolation enforced

⸻

Cost Summary

Infrastructure (per client, at 5K supporters)
	•	Anthropic Claude API (Sonnet 4): ~$200/mo
	•	Make.com (~150K ops): ~$137/mo
	•	Airtable Business: ~$45/mo
	•	OpenAI API (embeddings): ~$3/mo
	•	Pinecone: ~$0-35/mo
	•	Vercel Pro (amortized across clients): ~$20/mo
	•	Total per-client COGS: ~$405-440/mo

Shared infrastructure: Vercel Pro ($60/mo for 3 projects), Doppler (free), Clerk (free), Resend (free)

For full unit economics, see AI4Love-Pricing-Model.md.

Development tools: Windsurf Pro, Claude Max, ChatGPT Plus, Gemini Pro
Communication: Zoho Workplace
Research: Perplexity Pro

⸻

Implementation (3 Weeks)

Week 1: Data Mapping and Integration
	•	Create Airtable base from template
	•	Clone Make.com scenarios, configure org credentials
	•	Connect integrations via Nango OAuth
	•	Normalize supporter records into unified Participation stream

Week 2: Agent Calibration and First Insights
	•	Agents run against real data
	•	Thresholds tuned to organization patterns
	•	Results validated against team judgment
	•	Knowledge vault seeded with org documents

Week 3: Team Access and Training
	•	MCP connections provisioned for staff
	•	Dashboard access configured
	•	Weekly rhythm established (Monday review of top insights, daily MCP check)
	•	Internal champion identified (usually Development Director)

⸻

Final Position

AI4Love is a normalized shadow intelligence layer.

It does not replace systems of record.
It does not automate supporter outreach.
It detects patterns across systems that humans cannot manually surface.

It strengthens human relationships.
