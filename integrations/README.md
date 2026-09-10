# Integrations

Current build status for platform connectors. Source: AI4Love API Integration Status, February 2026.

## Summary

| Status | Count |
|---|---|
| Full | 19 |
| Partial | 5 |
| None | 2 |
| Event only | 1 |
| Total | 27 |

## Donor management

| Platform | Status |
|---|---|
| Blackbaud RE NXT | Full |
| DonorPerfect | Full |
| Bloomerang | Full |
| Virtuous | Full |
| Classy | Full |
| EveryAction | Full |
| Neon CRM | Full |
| GivingData | Full |

## CRM and engagement

| Platform | Status |
|---|---|
| Salesforce | Full |
| HubSpot | Full |
| Wild Apricot | Full |
| NationBuilder | Partial |
| Foundant GLM | Partial |

## Email and marketing

| Platform | Status |
|---|---|
| Mailchimp | Full |

## Events and volunteers

| Platform | Status |
|---|---|
| Eventbrite | Full |
| Galaxy Digital | Full |
| Better Impact | Partial |
| RunSignUp | Partial |

## Finance and payments

| Platform | Status |
|---|---|
| Stripe | Full |
| QuickBooks | Full |
| Xero | Full |
| Fluxx | Full |
| PayPal | Partial |

## Data enrichment

| Platform | Status | Notes |
|---|---|---|
| Environics Analytics | Full | Canadian postal codes only |

## Other

| Platform | Status |
|---|---|
| Instrumentl | None |
| PayPal Giving Fund | None |
| Looker Studio | Event only |

## Connection architecture

All integrations are owned per organization. Nango handles OAuth at the dashboard Integrations page. Make.com pulls credentials from Nango when running syncs. AI4Love never handles vendor credentials directly. Bounded custody: read-only sources, one isolated working base per organization deleted after the exit window (System Spec v3.4 section 1).
