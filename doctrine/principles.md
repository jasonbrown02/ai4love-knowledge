# AI4Love Doctrine: 5 Principles

Draft. Status: needs refinement during Pass B / Pass C work.

These principles are designed so a nonprofit could adopt them manually without AI4Love's product. They describe how relationship intelligence should work, not which tool delivers it.

---

## 1. Relationship signals already exist. Fragmentation hides them.

Every system a nonprofit uses already captures signals about supporter relationships. Donation history, volunteer hours, event attendance, email engagement, social interactions. The signals exist. They sit in separate systems that do not talk to each other. The work is connecting what you already have, not collecting more.

## 2. Detect patterns deterministically. Generate narrative selectively.

A pattern is either present or it is not. Pattern detection should be rule-based and auditable. AI is for translating detected patterns into language a human can act on, not for deciding which supporters matter.

## 3. Silence beats incorrect output.

When confidence is low, say nothing. A missed insight costs less than a wrong insight presented as fact. Suppression is a feature.

## 4. Humans remain responsible for outreach.

No supporter should receive a message a human did not write and approve. Restraint protects institutional trust. Automation belongs in internal workflows, never in donor-facing communication.

## 5. Relationships, not conversions.

Supporters are people in relationship with your organization, not conversion targets. Optimize for relationship continuity, not transaction frequency. The work compounds.

---

## How these connect to the product

- Principle 1 → unified Participation model
- Principle 2 → deterministic pattern detection, LLM for narrative only
- Principle 3 → suppression gates, NO_INSIGHT returns
- Principle 4 → the three refusals (no write-back, no campaigns, no sending)
- Principle 5 → recency-based health buckets, no conversion-rate optimization

## The three-layer model (operational expression of the doctrine)

Source: System Spec v3.2 section 3.

**Layer 1: Deterministic Analysis (rule-based)**
Nine nightly agents via Make.com apply fixed math. RFM scoring, rolling averages, decay functions, threshold triggers. This is not AI. It is rollups, formulas, and conditional logic.

**Layer 2: Text Generation (LLM-constrained)**
Claude API writes human-readable insight text after Layer 1 pattern detection. The LLM receives only supporter name, detected pattern type, relevant metrics, and full pre-fetched timeline. The LLM cannot access full records, trigger actions, or override suppression rules. Content Integrity Policy (v2026-04-07) is enforced. Post-generation verification cross-checks AI-claimed metrics against actual Airtable data.

**Layer 3: Human Action**
Staff review dashboard insights and decide whether to act. No automated outreach. No loop closure.

The principle that ties it together: **suppression over speculation. Silence is safer than noise.**
