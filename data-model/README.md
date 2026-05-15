# Data Model

Reference for AI4Love's canonical data structures. Source: System Spec v3.2, May 12, 2026.

## Files

- [status-thresholds.md](status-thresholds.md) — Supporter status thresholds (Active, Steady, Cooling, At-Risk, Lapsed)

## Core entities (summary)

**People** — Root identity table. Unique by email. Demographic fields and rollups.

**Participation** — Canonical activity stream. Every donation, volunteer act, or engagement maps here. Primary analytic date: `participated_at`. Hosts `agent_queue_status` field for nightly agent eligibility filtering.

**Donors / Volunteers / Engagements** — Raw source tables only. No AI-generated fields.

**Events** — Optional structured activity grouping.

**Insights** — All AI outputs. One insight record per pattern per person. Attaches to People, not Participation.

## Ten design principles

1. People is the root entity. Every insight belongs to a person.
2. Participation is the unified activity stream.
3. `participated_at` drives time analysis. Never use `created_at`.
4. Insights attach to People, not Participation.
5. No AI fields in source tables.
6. Identity flows through link fields only.
7. All metrics derive from formulas or rollups.
8. `agent_queue_status` lives on Participation (moved from People Feb 2026).
9. Health buckets derive from `days_since_last_activity`, not Airtable status.
10. Nurture handles groups. Connect handles individuals.

## Source of truth

AI4Love System Spec v3.2, sections 4-5.
