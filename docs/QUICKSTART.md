# Quickstart — First production run in 48 hours

This walks you from a cold clone to your first graded LinkedIn post. Assumes you've installed the skill system per the main [README](../README.md).

---

## Day 1: Foundation (30-60 min)

### 1. Create the client folder

```bash
cp -r templates/client-folder-template clients/<person_name>/content
```

The folder has placeholders for:
- `client-profile.md` — who they are, what they sell, posting cadence
- `voice-profile.md` — populated by the voice interview in step 2
- `icp.md` — 3 buyer tiers with pain language
- `content-pillars.md` — 3-5 themes with goals and funnel stage
- `cta-templates.md` — CTA types mapped to post categories
- `brand-guidelines.md` — visual style, formatting preferences
- `influencer-list.md` — **client fills this in:** 15-25 LinkedIn profiles tiered 1-3. Required for the weekly industry analysis.
- `learning-log.md` — auto-populated over time
- `transcripts/` — drop call recordings here (optional but high-signal)

### 2. Run the voice interview

In Claude Code, invoke:

```
Run the skill at ./skills/01-voice-profile.md for client <person_name>
```

This runs a **25-question conversation** — not a form. It captures:
- How they actually talk (sentence rhythm, vocabulary, humor)
- What they believe (strong opinions, hills they'll die on)
- Their hard NOs (what they refuse to say, topics they won't touch)
- Who they're writing for (ICP pain language in the person's own words)

**Do the interview properly. Don't rush it.** The voice profile is the guardrail for every draft going forward. If it's thin, every post will sound like AI.

Outputs land in the client folder. Review them before moving on.

### 2b. Fill in the influencer list

Open `clients/<person_name>/content/influencer-list.md` and have the client fill it in:
- **Tier 1** (5-10): direct competitors / category leaders their ICP already follows
- **Tier 2** (5-10): adjacent voices speaking to the same buyer
- **Tier 3** (3-5): aspirational / broader category
- **Off-limits**: anyone whose tactics violate the voice profile's hard NOs

This list is the engine behind the weekly industry analysis (step 4 below). LinkedIn URL is required for each entry — the Apify scrape uses it directly. Refresh quarterly.

---

## Day 2: First production run (2-3 hours, most of it parallel)

### 3. Run the pre-flight system check (2 min)

```
Run ./maintenance/system-check.md
```

Confirms env vars, API tokens, and external dependencies are wired up. Pass/fail checklist. Don't skip — catches broken runs before you start.

### 4. Weekly industry analysis — run this FIRST every week

```
Run ./skills/weekly-influencer-analysis.md for client <person_name>
```

Scrapes the last 7 days of posts across every influencer in `influencer-list.md` (one batched Apify run), then:

- Ranks every post by **Engagement Score** = `(likes) + (3 × comments) + (5 × shares)`
- Flags **outliers** — posts with a Z-score ≥ 2.0 against the author's own median (i.e. 2x+ above their normal performance)
- Classifies each hook against the 50-template library + 5 creator-benchmark patterns (hidden truth, `[X] of [Y]`, number-led, cliffhanger, contrarian)
- Clusters topics against the client's content pillars
- Tracks format mix (carousel / image / video / text) and length distribution
- Cross-references against `creator-benchmark.md` baselines to flag patterns performing above **or below** historical norms
- Surfaces gaps — pillars nobody covered this week, topics everyone took from the same angle

Output: `clients/<person_name>/content/weekly-intel/{{YYYY-MM-DD}}.md` — a ranked brief with top 10 posts, hook patterns, topic clusters, format trends, outlier hypotheses, gaps, and 3-5 concrete recommendations for the ideation session.

Every 4th run also produces a **Trend Memory** summary that tracks which patterns are holding, fading, or emerging across the last 4 weeks.

### 5. Weekly research workers (runs in ~10 min, mostly parallel)

```
Run ./skills/02-research-workers.md for client <person_name>
```

Six workers fire in parallel:
1. LinkedIn trend scrape (Apify) — broad un-curated niche scan (complements step 4)
2. Reddit audience mining
3. YouTube long-form mining (Gemini)
4. X/Twitter signal
5. Fireflies transcripts (if you have client calls recorded)
6. Repurposing archive (this person's own post history)

Output: deduplicated, quality-gated signal report — merged with the weekly intel brief from step 4.

### 6. Ideation — ranked idea batch

```
Run ./skills/03-weekly-ideation.md
```

Takes the weekly intel brief + research output, generates a ranked batch of content ideas. Each idea is scored against ICP relevance, mapped to a content pillar, and sized to the person's posting cadence. **You pick which ones to develop.**

### 7. Hooks (per approved idea)

```
Run ./skills/04-hook-generator.md for idea <idea_id>
```

Generates 20+ hook variations from a 50-template library grouped by emotional trigger (desire / curiosity / fear). Informed by the 366-post creator benchmark **and this week's top-performing patterns from the influencer analysis.** **You pick the strongest opening.**

### 8. Copy (per approved hook)

```
Run ./skills/05-copy-developer.md for idea <idea_id> using hook <hook_id>
```

Full draft in documented voice. Follows the data-backed writing rules from the creator benchmark (one thought per line, bold unicode headers, arrow bullets, listicle structure, 800-1500 chars, no emojis in hooks, etc.).

### 9. Grade + refine

```
Run ./skills/06-post-grader.md for draft <draft_id>
```

5-dimension rubric, scored /50:
| Dimension | Max | Measures |
|---|---|---|
| Hook strength | /10 | Would you stop scrolling? |
| Voice match | /10 | Does it sound like the person? |
| ICP relevance | /10 | Does the target buyer care? |
| Structure & retention | /10 | Does it retain to the end? |
| Reward & CTA | /10 | Does it deliver + close well? |

Below 38/50 → auto-rewrite with dimension-specific fixes. Max 2 rewrite loops. Still fails? Flagged for human review.

### 10. Deliver

```
Run ./skills/07-deliver-schedule.md for draft <draft_id>
```

Packages approved post with copy + visual brief + scheduling notes → ClickUp (client approval) → Taplio (LinkedIn scheduling). Performance data flows back into the learning log on the next cycle.

---

## Day 3+ and beyond

- **Every week, same day, before ideation:** re-run `./skills/weekly-influencer-analysis.md`. Consistency is what makes the trend signal meaningful — run it Monday every Monday, not "whenever."
- **Every 4 weeks:** the weekly analysis skill auto-produces a **Trend Memory** summary of patterns holding, fading, or emerging across the last 4 briefs.
- **Every 5 sessions:** run `./maintenance/pattern-recognition.md` — reads the learning log, flags voice drift, suggests skill updates.
- **Monthly:** run `./maintenance/content-auditor.md` — full strategy audit.
- **Quarterly:** refresh `influencer-list.md`. Drop anyone the client no longer tracks, add new voices. A 12-month-stale list models yesterday's winners.
- **When a post performs:** run `./skills/08-repurpose.md` — turns one validated LinkedIn post into 5 platform-native pieces (X thread, newsletter, SEO blog, short-form video script, carousel).

---

## Troubleshooting

**"Voice profile is thin / all the drafts sound generic."**
You rushed the voice interview. Redo it. The voice profile is the single highest-leverage document in the system.

**"Research workers are returning empty results."**
Most likely missing API keys. Run `./maintenance/system-check.md` first. If an API is not available, that worker no-ops — other workers still run.

**"Posts keep failing the grader at the same dimension."**
Good — the learning log is working. Read `clients/<person>/content/learning-log.md`, look at what fails repeatedly, update the corresponding foundation doc (usually voice-profile or content-pillars).

**"Posts pass the grader but don't perform on LinkedIn."**
The grader is a proxy for quality, not a guarantee of engagement. Feed real performance data back via `./skills/07-deliver-schedule.md`. Over time the learning log catches the gap.

**"The weekly brief looks the same every week."**
Your influencer list is too narrow — probably all Tier 1 (direct competitors who all think the same way). Widen it with 3-5 Tier 2 and Tier 3 voices and re-run.

**"Apify run aborts or times out."**
Usually caused by `scrapeReactions: true` (bloats the dataset 100x) or batching too many profiles in one run. Keep reactions off and cap at ~25 profiles per run.

**"No outliers ever show up in the brief."**
The Z-score calc needs post history to establish the author's median. Once per quarter, run a deeper scrape (`maxPosts: 20` instead of 10) to rebuild baselines.
