# AI4Love | Social Intelligence Module
**Premium Add-On Brief**
**Status:** Product brief; implementation is configured per client
**Last updated:** June 22, 2026

---

## What It Is

The Social Intelligence Module connects your organization's owned social channels to AI4Love's Insights Engine. It surfaces patterns between your public social performance and your supporter relationship data.

This is not a social media management tool. It does not schedule posts or manage content. It tells you what your social activity reveals about your supporter community and where the two overlap.

---

## Supported Platforms

Planned production connections use OAuth where the platform supports it. Availability depends on platform API access and client configuration. Your organization controls access and can revoke it at any time.

| Platform | Data Available |
|---|---|
| Facebook | Page views, post engagement, follower growth, audience demographics, link clicks |
| Instagram | Reach, impressions, story performance, reel views, follower trends (via Meta Graph API) |
| LinkedIn | Company page followers, post engagement, visitor demographics, content performance |
| YouTube | Channel views, watch time, subscriber growth, top-performing videos |
| X (Twitter) | Page-level engagement and follower data (paid API tier required) |

---

## What AI4Love Surfaces

The module adds social performance data as a new layer in the Insights Engine. Agents correlate social signals with supporter behavior patterns your team cannot manually connect.

| Social Signal | What AI4Love Surfaces |
|---|---|
| Post engagement spike on a specific program | Which donor segments engaged that same week |
| Follower growth slows during a campaign gap | At-risk supporters who went quiet in the same period |
| Video content outperforms text posts | Volunteer recruitment patterns tied to video reach |
| Low engagement on a major campaign post | Whether the signal shows up in donation behavior |
| High reach with low click-through | Supporters who saw your content but did not convert to action |

---

## How It Works

The module fits cleanly into the existing AI4Love architecture.

- Your organization connects social accounts via the AI4Love Integrations page.
- Nango handles OAuth. AI4Love never stores your credentials.
- Make.com pulls social performance data on a nightly schedule.
- Data normalizes into the Social Metrics table alongside, but not inside, the person-level Participation model.
- Agent 0 generates an organization-level Community Vibe snapshot. When vibe injection is enabled, the seven core analysis agents may use that snapshot for narrative context without changing eligibility, scoring, or suppression logic.
- Your team reviews findings in the dashboard. No automated posting. No automated outreach.

---

## What It Is Not

- It does not access individual supporter social profiles. It works only with data from your own connected pages.
- It does not post, schedule, or manage social content.
- It does not track or monitor supporters across social platforms.
- It does not replace a social media management tool like Hootsuite or Buffer.

---

## Pricing and Availability

The Social Intelligence Module is a premium add-on, priced separately from the AI4Love core platform. It is designed for organizations ready to connect their public presence to their relationship data and extract cross-channel intelligence.

| | |
|---|---|
| Availability | Planned for Phase 2 client onboarding |
| Pricing model | Monthly add-on, per organization |
| Onboarding | OAuth setup + 30-day baseline data collection before insights activate |
| Minimum requirement | Active AI4Love core subscription |
| Platforms included | Up to 3 connected channels per organization at base tier |

---

*This document is a product brief for internal use and prospect conversations. Pricing and availability subject to change.*

*AI4Love | jason@ai4love.ca | ai4love.ca*
