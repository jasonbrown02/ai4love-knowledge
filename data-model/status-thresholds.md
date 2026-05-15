# Supporter Status Thresholds

Derived from `days_since_last_activity` across the full Participation stream. Drives the Nurture dashboard health spectrum and several agent eligibility gates.

## Thresholds

| Status | Days since last activity | Notes |
|---|---|---|
| Active | Under 90 days | Engaged in last quarter |
| Steady | 91 to 180 days | Slowing but recent |
| Cooling | 181 to 365 days | Within a year but quieting |
| At-Risk | 366 to 730 days | Drifting; primary Agent 1 cohort |
| Lapsed | 731+ days | Long-gone; primary Agent 9 cohort (with $500+ lifetime giving filter) |

## Where these appear

**Nurture dashboard health spectrum:** Thriving, Steady, Cooling, At-Risk, Lapsed (Thriving maps to Active in this context).

**Agent 1 (At-Risk Detection):** flags supporters entering the At-Risk band.

**Agent 9 (Lapsed Donor Resurrection):** filters Lapsed band by lifetime giving ≥ $500 and applies six detection patterns.

**Agent 9b (Recurring Pause Resurrection):** filters supporters with 1+ year since last donation, proven recurring history (3+ monthly gifts), $200+ lifetime.

## Calculation principle

All status derives from `days_since_last_activity`, never from Airtable status fields. This means status reflects actual recency, not stale manual entries.

The full Participation stream means donations + volunteer acts + engagements all count. A supporter who hasn't donated in 2 years but volunteered last month is Active, not Lapsed.

## Source

AI4Love System Spec v3.2, section 6.
