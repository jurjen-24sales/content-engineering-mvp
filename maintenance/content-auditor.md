---
name: content-auditor
description: Monthly full strategy audit. Checks pillar relevance, voice freshness, performance patterns. Outputs prioritized maintenance report with ranked fixes.
version: 1.0.0
---

# Content Auditor

## Purpose

Full strategy audit run monthly. Checks whether the content engine is still aligned with where the market and the client's business have moved. Outputs a prioritized maintenance report.

## When to Run

- Monthly (end of month, after performance data is collected)
- After a major client business change (new role, funding, ICP shift)
- When engagement metrics show sustained decline (3+ weeks)

## Prerequisites

- Client's full content folder (all .md files)
- Learning log with performance data (minimum 1 month)
- Pattern recognition output (if available)
- Access to recent Fireflies transcripts (for voice freshness check)

---

## Audit Checklist

### 1. Pillar Relevance

- Are the current 3-5 content pillars still aligned with the client's business direction?
- Has the market shifted? Are competitors talking about topics the pillars don't cover?
- Are any pillars consistently underperforming? (check performance data)
- Has the client entered a new market, launched a new product, or shifted ICP?

**Decision:** Keep / Evolve / Replace / Add pillar

### 2. Voice Freshness

- Pull 3-5 recent Fireflies transcripts
- Compare natural speech against voice profile
- Has the client's vocabulary evolved?
- Are they talking about new topics not captured in the profile?
- Has their confidence/tone shifted?

**Decision:** No update needed / Minor refresh / Full 25-question re-interview

### 3. ICP Accuracy

- Are the 3 buyer tiers still correct?
- Has the client's customer base changed?
- Are the documented pain points still current?
- Is the language map still accurate (marketer words vs buyer words)?

**Decision:** Current / Needs minor update / Needs major revision

### 4. Performance Patterns

- Overall engagement trend (up/flat/down over 90 days)
- Follower growth rate vs previous period
- Which content types are trending up vs down?
- Which posting times are performing best?
- Are lead magnets converting?

### 5. Competitive Landscape

- What are the client's top 5 industry influencers posting about?
- Any new voices gaining traction in the niche?
- Has the competitive content landscape shifted?
- Are there new formats or approaches worth testing?

### 6. Foundation Doc Health

For each foundation doc, check:
- `client-profile.md` — still accurate?
- `voice-profile.md` — still fresh?
- `icp.md` — still current?
- `content-pillars.md` — still relevant?
- `cta-templates.md` — still converting?
- `brand-guidelines.md` — any visual changes?
- `learning-log.md` — being updated consistently?

---

## Output Format

```
CONTENT AUDIT — {{client_name}} — {{month}} {{year}}

EXECUTIVE SUMMARY:
{{2-3 sentence overview of content health}}

PILLAR HEALTH:
| Pillar | Status | Avg Engagement | Recommendation |
|--------|--------|----------------|----------------|
| {{pillar}} | {{green/yellow/red}} | {{n}} | {{keep/evolve/replace}} |

VOICE HEALTH: {{Fresh / Stale / Drifting}}
- {{specific findings}}
- Action: {{recommendation}}

ICP HEALTH: {{Current / Needs Update}}
- {{specific findings}}
- Action: {{recommendation}}

PERFORMANCE SUMMARY:
- Engagement trend: {{up/flat/down}} ({{%}} change)
- Follower growth: {{n}} ({{%}} rate)
- Best performing: {{type/pillar/hook}}
- Worst performing: {{type/pillar/hook}}

PRIORITIZED FIXES:
1. [{{priority}}] {{fix}} — Impact: {{expected improvement}}
2. [{{priority}}] {{fix}} — Impact: {{expected improvement}}
3. [{{priority}}] {{fix}} — Impact: {{expected improvement}}

NEXT MONTH FOCUS:
- {{specific recommendation for next month's content strategy}}
```
