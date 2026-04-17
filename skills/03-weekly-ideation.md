---
name: weekly-ideation
description: Weekly idea session — takes research output, runs quality gate + ICP tier scoring, outputs ranked idea batch sized to posting cadence.
version: 1.0.0
---

# Weekly Ideation Session

## Purpose

Turn raw research into a ranked batch of content ideas. Quality gate + ICP tier scoring + pillar mapping. Sized to the client's posting cadence.

## When to Run

- Weekly, after research workers complete (Step 3 in pipeline)
- Ad-hoc when content calendar needs refilling

## Prerequisites

- Research output from the 6 workers (merged, quality-gated)
- Client's `content-pillars.md`
- Client's `icp.md`
- Client's `learning-log.md` (to avoid repeating underperforming angles)
- Client's posting cadence (from `client-profile.md`)

---

## Process

### Step 1: Idea Generation

From the research output, generate content ideas using the 5 topic categories:

| Category | Source | Best For |
|----------|--------|----------|
| **Far Past** | Important lessons, career stories | Deep value, trust-building |
| **Recent Past** | Last week's calls, meetings, client interactions | Freshness, relevance |
| **Present** | Ideas captured in real-time from research | Authenticity |
| **Trending** | Current events intersecting the niche | Broader reach |
| **Manufactured** | Experiments or frameworks built to create content about | Biggest potential |

For each idea, capture:
```
Idea: {{one-line description}}
Category: {{Far Past / Recent Past / Present / Trending / Manufactured}}
Source: {{which research worker surfaced this}}
Pillar: {{which content pillar it maps to}}
ICP Tier: {{which buyer tier this serves — 1/2/3}}
Post type: {{Playbook / Listicle / Contrarian / Behind-the-Scenes / Case Study / Tool Stack}}
Signal strength: {{how many research sources confirmed this topic}}
```

**Target:** Generate 2-3x the posting cadence in ideas. If cadence = 4 posts/week, generate 8-12 ideas.

### Step 2: Quality Gate

Score each idea on 5 criteria:

| Criteria | Weight | Scoring |
|----------|--------|---------|
| ICP pain match | 25% | Does this address a documented pain point? (from icp.md) |
| Pillar alignment | 20% | Does it trace to a content pillar? No random acts of content. |
| Freshness | 20% | Has this been covered recently? Check learning log. |
| Signal strength | 20% | How many research sources confirmed this topic? |
| Content potential | 15% | Can this become a strong post? Is there enough substance? |

**Gate:** Ideas scoring below 60% get dropped. Don't force weak ideas into the batch.

### Step 3: ICP Tier Scoring

For each passing idea, score ICP tier targeting:

- **Tier 1 (Decision Makers):** Will a CEO/VP/CRO engage with this?
- **Tier 2 (Champions):** Will a Director/Manager share this internally?
- **Tier 3 (Practitioners):** Will an individual contributor save this?

Assign primary and secondary tier. Posts should have a clear primary audience.

### Step 4: Pillar Distribution Check

Compare idea batch against target pillar distribution from `content-pillars.md`.

If a pillar is underrepresented:
- Flag the gap
- Generate 1-2 additional ideas specifically for that pillar
- Pull from research archive or learning log refresh candidates

If a pillar is overrepresented:
- Deprioritize the weakest ideas in that pillar
- Check if the pillar itself needs splitting (content auditor territory)

### Step 5: Rank & Size

Rank all passing ideas by quality gate score. Size the batch to the posting cadence:

| Cadence | Batch size | Buffer |
|---------|-----------|--------|
| 3 posts/week | 3 ideas | +1 backup |
| 5 posts/week | 5 ideas | +2 backup |
| Daily | 7 ideas | +3 backup |

The buffer exists for ideas that fail in the hook or copy stage.

### Step 6: Assign Post Types

Map each idea to a LinkedIn post archetype:

| Archetype | When to use |
|-----------|-------------|
| **Playbook/Process** | Teaching a workflow or system |
| **Listicle** | Multiple items with brief explanations |
| **Contrarian Take** | Challenging a belief with evidence |
| **Behind-the-Scenes** | Revealing how something was built |
| **Case Study** | Company name + specific result |
| **Tool Stack** | Categorized list of tools/resources |
| **Story** | Personal experience with a lesson |

---

## Output Format

```
WEEKLY IDEA BATCH — {{client_name}} — Week of {{date}}
Posting cadence: {{n}} posts/week
Ideas generated: {{total}} | Passed quality gate: {{n}} | Final batch: {{n}}

BATCH (ranked by quality score):

1. {{idea title}}
   Category: {{category}} | Pillar: {{pillar}} | ICP Tier: {{tier}}
   Post type: {{archetype}} | Quality score: {{score}}%
   Source: {{research worker(s)}}
   Brief: {{2-3 sentence description of the post angle}}

2. {{idea title}}
   ...

BACKUP IDEAS:
{{1-3 backup ideas in same format}}

PILLAR DISTRIBUTION:
{{pillar_1}}: {{n}} posts (target: {{n}})
{{pillar_2}}: {{n}} posts (target: {{n}})
{{pillar_3}}: {{n}} posts (target: {{n}})

GAPS FLAGGED:
- {{any pillar or tier imbalances}}
```

---

## Ideation Anti-Patterns

- **No random acts of content.** Every idea must trace to a pillar. If it doesn't fit a pillar, either the idea is off-strategy or the pillars need updating.
- **No recycling underperformers.** Check the learning log before approving ideas. If a similar angle scored poorly before, either find a better angle or drop it.
- **No tier 3 overload.** Practitioner content is easy to generate but doesn't drive revenue. Keep tier 1 + tier 2 as primary targets.
- **No trend-chasing without a take.** A trending topic without the client's POV is just noise. The trend is the door; their unique angle is the content.
