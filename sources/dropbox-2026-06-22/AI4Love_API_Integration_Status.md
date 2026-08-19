# AI4Love API Integration Status
Purpose: Current status for 27 tracked platforms: 23 code-backed connector modules plus 4 planned, event-only, or externally implemented platforms. Update this file as integrations are completed or change status.

Last updated: June 22, 2026

## Status definitions
Full: Integration is complete. Field mapping, sync logic, dedup, and agent queuing all working.
Partial: Integration exists but is incomplete. Missing fields, edge cases, or sync gaps remain.
None: Integration not yet built.
Event only: Limited to a specific data type or trigger only.

## Implementation scope
- Code-backed means a connector service and mounted integration route exist in the ai4love repository.
- External/Make means the integration may exist outside this repository and must name its owning scenario or system before being treated as production-ready.
- None and Event only entries are tracked roadmap items, not part of the 23 code-backed connector modules.

---

## Donor Management

| Platform | Status | Notes |
|----------|--------|-------|
| Blackbaud RE NXT | Full | |
| DonorPerfect | Full | |
| Bloomerang | Full | |
| Virtuous | Full | |
| Classy | Full | |
| EveryAction | Full | |
| Neon CRM (Neon One) | Full | |
| GivingData | Full | |

## CRM and Engagement

| Platform | Status | Notes |
|----------|--------|-------|
| Salesforce | Full | |
| HubSpot | Full | |
| NationBuilder | Partial | |
| Wild Apricot | Full | |
| Foundant GLM | Partial | |

## Email and Marketing

| Platform | Status | Notes |
|----------|--------|-------|
| Mailchimp | Full | |

## Events and Volunteers

| Platform | Status | Notes |
|----------|--------|-------|
| Eventbrite | Full | |
| Galaxy Digital | Full | |
| Better Impact | Partial | |
| RunSignUp | Partial | External/Make implementation; no backend connector module exists in the ai4love repository. |

## Finance and Payments

| Platform | Status | Notes |
|----------|--------|-------|
| Stripe | Full | |
| PayPal | Partial | |
| QuickBooks | Full | |
| Xero | Full | |
| Fluxx | Full | |

## Data Enrichment

| Platform | Status | Notes |
|----------|--------|-------|
| Environics Analytics | Full | Canadian postal codes only. Returns null for non-Canadian addresses. |

## Other

| Platform | Status | Notes |
|----------|--------|-------|
| Instrumentl | None | |
| PayPal Giving Fund | None | |
| Looker Studio | Event only | Limited to event-level data trigger only. |

---

## Summary

| Status | Count |
|--------|-------|
| Full | 19 |
| Partial | 5 |
| None | 2 |
| Event only | 1 |
| Total | 27 |

## Implementation summary

| Scope | Count |
|-------|-------|
| Code-backed connector modules | 23 |
| External/Make partial connector | 1 |
| Planned or event-only entries | 3 |
| Total platforms tracked | 27 |
