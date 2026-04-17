---
name: weekly-influencer-analysis
description: Weekly industry-level content analysis. Scrapes client-supplied top influencers via Apify, ranks posts by engagement, extracts performing hooks, topics, formats, and lengths, classifies against the hook library and creator benchmark. Outputs a ranked Weekly Intel Brief that feeds ideation.
version: 1.0.0
---

# Weekly Influencer Analysis

## Purpose

Every week, answer one question: **what's working in this client's industry right now, and why?**

Input: a curated list of top influencers the client inserted.
Output: a ranked, engagement-weighted brief of hooks, topics, formats, and outliers — used as the primary fuel for the next ideation session.

This skill does **not** do broad LinkedIn scraping — that's Worker 1 in `02-research-workers.md`. This one is focused, deep, and weekly: the same curated list, analyzed the same way, every week. That consistency is what makes the trend signal meaningful.

## When to Run

- **Weekly, automatically** — same day every week (e.g., Monday morning, before the ideation session)
- Ad-hoc when a specific influencer publishes something high-signal
- Before onboarding a new client (baseline scan of their inserted list)

## Prerequisites

- `clients/{{client}}/content/influencer-list.md` — **client-supplied** list of 15-25 top influencers (see format below)
- Apify API token (env var `APIFY_TOKEN` or `~/.apify/auth.json`)
- Client's `icp.md` and `content-pillars.md` (for relevance filtering)
- `creator-benchmark.md` at repo root (baseline engagement + hook taxonomy)

---

## Step 1: Influencer list format

The client inserts their top influencers into `clients/{{client}}/content/influencer-list.md`. Format:

```markdown
# Influencer List — {{client_name}}

## Tier 1 — Direct competitors / category leaders
- [Name] — https://www.linkedin.com/in/{{handle}}/ — why they matter: {{1 line}}
- [Name] — https://www.linkedin.com/in/{{handle}}/ — why they matter: {{1 line}}

## Tier 2 — Adjacent voices / thought leaders
- [Name] — https://www.linkedin.com/in/{{handle}}/ — why they matter: {{1 line}}

## Tier 3 — Aspirational / broader category
- [Name] — https://www.linkedin.com/in/{{handle}}/ — why they matter: {{1 line}}

## Off-limits — do not model after
- [Name] — reason: {{1 line}}
```

**Rules:**
- 15-25 total (5-10 per tier)
- LinkedIn URL required — no name-only entries
- Client must explain *why* each one is on the list (keeps the list honest)
- Refresh quarterly — drop anyone the client no longer tracks

---

## Step 2: Scrape (Apify)

**Actor:** `harvestapi/linkedin-profile-posts` (ID: `A3cAPGpwBEG8RJwse`)
**Endpoint:** `POST https://api.apify.com/v2/acts/A3cAPGpwBEG8RJwse/runs`
**Auth:** `Authorization: Bearer $APIFY_TOKEN`

**Payload (per run — one run covers all influencers in a single batch):**

```json
{
  "profileUrls": [
    "https://www.linkedin.com/in/{{handle_1}}/",
    "https://www.linkedin.com/in/{{handle_2}}/",
    "...all 15-25 from influencer-list.md..."
  ],
  "maxPosts": 10,
  "postedLimit": "week",
  "scrapeReactions": false,
  "scrapeComments": false,
  "includeReposts": false,
  "includeQuotePosts": true
}
```

**Important:**
- `scrapeReactions: false` — reactions bloat the dataset 100x and can abort the run
- `postedLimit: "week"` — only pull last 7 days
- `maxPosts: 10` — covers even highly active posters without over-scraping
- Poll `GET /runs/{{runId}}` until `status == "SUCCEEDED"`, then fetch the dataset via `GET /runs/{{runId}}/dataset/items`

**If a profile fails to scrape** (rate limit, private, renamed): log it in the brief under `Scrape failures`. Don't silently drop it.

---

## Step 3: Per-post engagement scoring

For every post returned, compute a single **Engagement Score**:

```
Engagement Score = (likes × 1) + (comments × 3) + (shares × 5)
```

Why weighted: comments signal active debate (3x); shares signal "my audience needs this" (5x). Raw likes alone reward passive approval and over-index on big-followed creators.

Also compute each post's **Z-score against that author's own median** (from the last 10 posts in the scrape):

```
Author-normalized Score = (Engagement Score − author_median) / author_stdev
```

Posts with Z ≥ 2.0 are **outliers** — 2x+ better than the author's normal performance. These are the most interesting posts of the week.

---

## Step 4: Extract and classify

For each post, extract:

| Field | How |
|---|---|
| Hook (first line) | First sentence or first line before `\n\n` |
| Hook pattern | Classify against the 50 templates in `04-hook-generator.md` AND the 5 patterns in `creator-benchmark.md` (hidden truth, "The [X] of [Y]", number-led, cliffhanger, contrarian) |
| Emotional trigger | Desire / Curiosity / Fear |
| Topic | 1-3 tag topic using client's `content-pillars.md` taxonomy |
| Structure | listicle / story / playbook / contrarian / case study / data drop |
| Format | image / carousel / video / text-only |
| Word count | Count |
| Has P.S. | Yes / No |
| Has comment-bait CTA | Yes / No ("comment X to get Y") |
| Emojis in hook | Yes / No |

Use the taxonomy from `creator-benchmark.md` — don't invent new categories. Consistent tagging week-over-week is what makes trend detection possible.

---

## Step 5: Aggregate — the Weekly Intel Brief

Output a single brief at `clients/{{client}}/content/weekly-intel/{{YYYY-MM-DD}}.md` with these sections:

### Section A: Top 10 posts of the week

Sorted by Engagement Score. For each:

```
1. [Author] — Engagement: 1,420 | Z-score: +2.3 (OUTLIER)
   Format: Carousel · Words: 182 · Topic: {{topic}} · Structure: Listicle
   Hook pattern: Number-led + cliffhanger
   Emotional trigger: Curiosity
   Hook: "5 GTM experiments I ran this quarter — #3 broke our pipeline."
   URL: https://www.linkedin.com/posts/...
   Why it worked: {{1-2 sentences — what is this post doing right}}
   Steal-worthy: {{specific element to adapt — hook pattern, structure angle, topic angle}}
```

### Section B: Hook patterns performing this week

Aggregate top 30 posts by hook pattern. For each pattern:

```
Number-led (used in 9 of 30 top posts) — avg engagement: 820 | avg Z: +1.4
Example: "7 ways I..." ({{author}}, {{engagement}})
Delta vs creator-benchmark baseline (261): +214% this week
```

Flag patterns that are **performing above OR below** their historical creator-benchmark baseline. A pattern dropping 40% below baseline this week is just as actionable as one spiking above.

### Section C: Topics gaining traction

Cluster the top 30 posts by topic. For each topic cluster with ≥ 3 posts:

```
Topic: "AI SDR economics" — 4 posts, avg engagement: 980
Angle spread: skepticism (2), playbook (1), data drop (1)
Gap: nobody took the "why this won't work" angle — {{client}} could own it
Pillar match: {{content pillar name}}
Freshness: this topic first appeared 3 weeks ago, engagement still rising
```

### Section D: Format + length trends this week

```
Format mix (top 30): Carousel 44% | Image 30% | Video 16% | Text-only 10%
Format winner: Carousel (avg 780) vs text-only (avg 310) — 2.5x gap
Length sweet spot this week: 900-1,400 chars (avg 720 engagement)
Shift vs last week: +12% longer on average — audience appetite for depth ↑
```

### Section E: Outliers (Z ≥ 2.0)

Dedicated section for every author-normalized outlier. These are the posts that **broke the author's own ceiling** — usually the most instructive signal of the week.

```
OUTLIER: {{author}} posted 3.1x above their own median
Hook: "{{first line}}"
What's different about this post vs their usual: {{specific observation —
new format, new topic, different structure, more vulnerable, contrarian, etc.}}
Hypothesis: {{why this broke out}}
Action: {{can this be adapted? test the same pattern next cycle?}}
```

### Section F: Gaps — what nobody is covering

Cross-reference top-post topics against `content-pillars.md`. Flag:
- Pillars with **zero coverage** in the influencer set this week (opportunity to own)
- Topics **3+ influencers covered** but from the same angle (opportunity for contrarian take)
- Questions raised in comments with no good answer yet (opportunity for a playbook post)

### Section G: Scrape failures

```
Failed to scrape (log for next run):
- {{name}} — {{reason: rate limit / private / renamed / deleted}}
```

### Section H: Next-cycle recommendations

Synthesize A-F into 3-5 concrete recommendations for the ideation session:

```
1. Test [hook pattern] this week — outperformed baseline by {{%}} across {{n}} influencers
2. Cover [topic] from [angle] — 4 influencers posted, all missed [specific angle]
3. Try [format] — {{%}} engagement lift vs text-only this week
4. Adapt outlier: {{author}}'s "{{hook}}" pattern — hypothesis matches our Tier 1 ICP pain
5. Avoid: [pattern that underperformed] — engagement dropped 30% below baseline
```

These recommendations become direct input to `./skills/03-weekly-ideation.md`.

---

## Step 6: Append to learning log

After the brief is written, append a one-line summary to `clients/{{client}}/content/learning-log.md`:

```
- {{YYYY-MM-DD}} WEEKLY-INTEL: {{top 3 findings in 1 line each}} [CONFIDENCE: HIGH if signal across 5+ posts, MED if 3-4, LOW if 1-2]
```

This builds the long-arc pattern memory — over 12 weeks, you'll see which trends held and which were noise.

---

## Trend Memory (every 4 weeks)

Every 4th run, cross-reference the last 4 briefs and surface:

```
PATTERN HOLDING: [pattern] has outperformed baseline 3+ weeks in a row — promote to permanent hook template rotation
PATTERN FADING: [pattern] outperformed 4 weeks ago, now below baseline — rotate out
TOPIC ARC: [topic] appeared weeks 1-2, peaked week 3, declining week 4 — timing window closed
EMERGING: [topic] first seen this week in 1 post, now in 4 — early signal, test fast
```

Write the trend-memory summary to `clients/{{client}}/content/weekly-intel/trend-memory-{{YYYY-MM-DD}}.md`.

---

## Guardrails

- **Never model after "off-limits" creators** from the influencer list. If one of them is posting about your client's topic, note it in Section F as a gap they could counter — don't copy their angle.
- **Don't optimize for the top 1 post** — optimize for the top 10. A single viral post is noise; repeating patterns across 10 posts are signal.
- **Engagement is a proxy for "people stopped scrolling," not "this is good content."** A 20K-like post shaming a competitor is high engagement and bad precedent. Use the `voice-profile.md` hard NOs to filter patterns that violate the client's standards, even if they performed.
- **Refresh the influencer list quarterly.** If a client's list is 12 months stale, the brief is modeling yesterday's winners.

---

## Failure modes (and fixes)

| Symptom | Cause | Fix |
|---|---|---|
| Brief is the same every week | Influencer list is too narrow / all-Tier-1 | Widen to Tier 2 + Tier 3, add 3-5 adjacent voices |
| No outliers ever | Author-normalized Z calc needs more history | Scrape `maxPosts: 20` once per quarter to rebuild medians |
| Hook patterns feel generic | Classification is too coarse | Add sub-patterns to `04-hook-generator.md` and re-tag |
| "Topics gaining traction" never clusters | Topic taxonomy in `content-pillars.md` is too abstract | Tighten pillars to specific sub-topics, re-run |
| Apify run aborts | `scrapeReactions` accidentally true, or too many profiles per run | Keep reactions off, batch ≤ 25 profiles per run |
