AI4Love Stack and Operating Reference
Purpose: LLM-readable reference for cost monitoring, tool prioritization, stack-first problem solving, and creative tool use patterns.

Last updated: March 2026

Companion Documents
For technical architecture and data model, see AI4Love_System_Spec_v3.1.md.
For product positioning, agents, and onboarding, see AI4Love-Product-Overview.md.
For pricing and unit economics, see AI4Love-Pricing-Model.md.

---

How to Use This Document

When Jason asks about tools, costs, or how to build something, reason in this order:

1. Can the existing stack solve this? Check Core Stack first.
2. Is there a free or included tool that covers it? Prefer those.
3. Is there an interesting or non-obvious way to use an existing tool? Explore that before suggesting new tools.
4. Only recommend a new paid tool if nothing in the stack covers the need. Always explain the reason.

---

Core Stack

Product Infrastructure

| Tool | Plan | Monthly Cost | Primary Role |
|------|------|-------------|--------------|
| Airtable | Business | ~45 USD/client | Central data hub, per-client base (125K records/base) |
| Vercel | Pro | 60 USD (3 projects) | Dashboard hosting (frontend), serverless API (backend), MCP server |
| Make.com | Core | ~11 USD + ops packs | Agent orchestration, integration syncs (~150K ops/mo at 5K supporters) |
| Anthropic Claude API | Usage | ~200 USD/client at 5K | Primary LLM — Sonnet 4 for all 7 agents, campaign generation |
| OpenAI API | Usage | ~3 USD/client at 5K | Embeddings only — text-embedding-3-large for Agent 7 vector search |
| Pinecone | Free/Starter | 0–35 USD | Vector database for KindMind research + per-client vault |
| Clerk | Free tier | 0 USD | Email-based authentication (10K MAU free) |
| Nango | Included | 0 USD | OAuth gateway for 23 client integration connectors |
| Doppler | Free tier | 0 USD | Secrets management, syncs env vars to Vercel |
| Resend | Free tier | 0 USD | Health alert emails |

Per-client COGS at 5,000 supporters: ~$405–440 USD/month
For full unit economics and margin analysis, see AI4Love-Pricing-Model.md.

Development Tools

| Tool | Plan | Monthly Cost | Primary Role |
|------|------|-------------|--------------|
| Windsurf | Pro | 17 USD | Primary IDE with Claude integration |
| Claude | Max | 140 USD | Primary LLM for planning, building, and reasoning |
| ChatGPT | Plus | 20 USD | Secondary LLM, alternative reasoning and drafting |
| Gemini Pro | Pro | 20 USD | Secondary LLM, research and cross-checking |

Development tools total: 197 USD per month

Communication

| Tool | Plan | Monthly Cost | Primary Role |
|------|------|-------------|--------------|
| Zoho Workplace | Paid | included | AI4Love email (jason@ai4love.ca, info@ai4love.ca) |

Research

| Tool | Plan | Monthly Cost | Primary Role |
|------|------|-------------|--------------|
| Perplexity Pro | Free until October 2026 | 0 USD | Deep research, source-cited answers |
| NotebookLM | Free | 0 USD | Document analysis, pattern finding across uploaded sources |

Available from Design Business (not in AI4Love costs)

| Tool | Role |
|------|------|
| Dropbox (paid) | Large file storage and secure client delivery |
| Adobe Creative Cloud | Professional design, print, and video output |
| Google Workspace (jason@jasonbrown.design) | Client collaboration, shared docs |

Free Infrastructure

| Tool | Role |
|------|------|
| GitHub | Version control, code storage |
| Notion | Documentation, specs, internal knowledge base |
| Figma | UI design and wireframing |
| Canva | Quick graphics and social assets |

---

Monthly Cost Summary

| Category | Monthly (platform only) | Notes |
|----------|------------------------|-------|
| Product infrastructure (shared) | ~80 USD | Vercel + Doppler + Clerk + Resend |
| Product infrastructure (per client) | ~405–440 USD | Anthropic + OpenAI + Make.com + Airtable + Pinecone |
| Development tools | ~197 USD | Windsurf + Claude + ChatGPT + Gemini |
| Communication | included | Zoho |
| Research | 0 USD | Perplexity + NotebookLM |

Note: Anthropic Claude API is the largest variable cost and scales with supporter count and daily activity rate. See AI4Love-Pricing-Model.md for COGS at 5K/10K/15K supporters.

---

Tool Priority Rules

When solving a problem or building a feature, follow this order:

1. Free or included tools first. GitHub, Notion, Figma, Canva, Perplexity, NotebookLM.
2. Existing paid stack second. Airtable, Make.com, Vercel, Claude, Windsurf, ChatGPT, Gemini.
3. Design business tools when relevant. Dropbox for large file delivery, Adobe for professional output, Google for client collaboration.
4. New paid tools only as a last resort. Must justify cost against existing stack gap.

---

Stack-First Problem Solving Patterns

Use these patterns before suggesting anything outside the current stack.

Need to store documents or research?
Use Notion for internal documentation. Use Pinecone (already running) for semantic search. Use Dropbox for large files or client-facing delivery.

Need to automate a workflow?
Use Make.com. It is already the orchestration engine. Build a new scenario rather than adding a new tool.

Need to analyze a set of documents together?
Use NotebookLM. Upload the documents and ask questions across them. Good for synthesizing multiple specs, research papers, or client materials into a single reasoning session.

Need to generate or test AI outputs?
Use Claude Max as primary. Cross-check with ChatGPT Plus or Gemini Pro for alternative perspectives. Use Perplexity for source-cited research to back recommendations.

Need to deliver something to a client?
Create in Adobe (professional output) or Google Docs (collaborative). Store and share via Dropbox. Send via Zoho (jason@ai4love.ca).

---

Interesting Tool Use Patterns

These are non-obvious ways to use existing tools that are worth exploring or referencing.

NotebookLM as a project brain
Upload all AI4Love spec docs, meeting notes, and research papers into a single NotebookLM. Use it as a persistent reasoning base that can answer questions across the entire document set. Good for onboarding new collaborators or preparing for client meetings without re-reading everything.

Perplexity for live sector research
Use Perplexity before seeding KindMind with new research. It surfaces recent, source-cited studies on donor psychology, volunteer engagement, and fundraising strategy that can be downloaded and added to the KindMind vector database.

Gemini Pro for cross-checking Claude outputs
When Claude produces a strategy recommendation or system design, run the same prompt through Gemini to surface alternative approaches or blind spots. Especially useful for architecture decisions.

Airtable as a lightweight CMS
Airtable can serve as a simple content management layer for dashboard copy, agent prompt templates, and configuration values. Avoids hardcoding content in code and makes it editable without a deployment.

Make.com as a test harness
Before building a full integration, use Make.com's HTTP module to manually trigger API calls against partner platforms. Faster than writing code to test endpoint responses.

Windsurf with Claude integration as a pair programmer
Windsurf's built-in Claude integration means the IDE understands the codebase context. Use it for refactoring, debugging, and generating boilerplate rather than switching between tools.

---

Practical Delivery Examples

Client deliverable (e.g. impact report PDF)
1. Create in Adobe InDesign. Export high quality PDF.
2. Store in Dropbox. Create password protected link with 60 day expiration.
3. Send via Zoho (jason@ai4love.ca) with AI4Love branding.

Collaborative planning with a foundation
1. Create Google Doc from jason@jasonbrown.design.
2. Share with foundation team for real time collaboration.
3. Store final version in Notion or GitHub for records.

Platform demo recording
1. Record with Loom or screen recorder.
2. Store video in Dropbox with password protected link and 30 day expiration.
3. Deliver via Zoho with a PDF one pager from Adobe.
