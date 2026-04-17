---
name: content-engine
description: Full content production engine — foundation, research, ideation, hooks, copy, grading, repurpose, delivery. Multi-client system with voice profiles, learning logs, and weekly influencer scanning. Based on ColdIQ methodology.
model: inherit
version: 1.0.0
---

## Context Dependencies

Load these knowledge base files when this skill is invoked:
- `knowledge_base/methodology/content-unit-framework.md` — Hook + Retain + Reward structure for every content piece
- `knowledge_base/methodology/content-scaling-strategy.md` — Depth-then-width scaling approach for multi-platform repurposing
- `knowledge_base/methodology/hormozi-content-structure-formula.md` — 4-part content formula for engagement and retention
- `knowledge_base/business/audience-as-compounding-asset.md` — Audience compounding model that grounds the content flywheel strategy


# Content Engine

One terminal. One engine. Many clients. Each person sounds like themselves at scale.

## When to Use This Skill

Use this skill to run the full content production pipeline for a client. This is the orchestrator — it chains the sub-skills in order.

**Do NOT use for:**
- One-off LinkedIn posts (overkill — write directly)
- Cold email copy (different pipeline, different discipline)
- Paid ad copy (different format, different psychology)

## Prerequisites

Before first production run, a client folder MUST exist with completed foundation docs:

```
clients/{{client_name}}/content/
├── client-profile.md        ✅ required
├── voice-profile.md          ✅ required (run voice-profile skill first)
├── icp.md                    ✅ required
├── content-pillars.md        ✅ required
├── cta-templates.md          ✅ required
├── brand-guidelines.md       ✅ required
├── learning-log.md           ✅ auto-generated
└── transcripts/              optional (Fireflies dumps)
```

If foundation docs don't exist, run **Step 1: Foundation** first. Don't skip this.

---

> **COMPOUND CHECK:** Before starting, read `clients/{{client}}/debrief-log.md` if it exists. Apply any lessons tagged for this skill.

## The Pipeline

```
Step 1        Step 2          Step 3         Step 4          Step 5         Step 6          Step 7
Foundation → Research → Ideation → Hooks → Copy → Grade+Refine → Deliver
(once)       (weekly)    (weekly)   (per idea)  (per idea)  (per draft)     (per batch)
```

### Step 1: Foundation (built once per person)

**Skill:** `./skills/01-voice-profile`

Run the 25-question voice conversation. This is NOT a form — it's a real conversation that captures how someone actually talks, their beliefs, humor, sentence rhythm, and hard NOs.

Outputs:
- `voice-profile.md` — the AI guardrail for every draft
- `icp.md` — 3 buyer tiers with pain language
- `content-pillars.md` — 3-5 themes with goals and funnel stages
- `cta-templates.md` — CTA types mapped to post categories
- `brand-guidelines.md` — visual style, formatting preferences

**Many people skip this and go straight to writing. Then wonder why everything sounds the same.**

### Step 2: Research (runs weekly)

**Skill:** `./skills/02-research-workers`

Six parallel research workers:

1. **Apify + LinkedIn scraping** — what's performing in your niche right now
2. **Reddit mining** — real audience pain language from niche communities
3. **YouTube mining (Gemini)** — frameworks from long-form video worth adapting
4. **X/Twitter signal** — live debates and hot takes this week
5. **Fireflies transcripts** — client call recordings turned into content gold (highest-signal source)
6. **Repurposing archive** — your own post history, what worked, what didn't

Plus: **Weekly influencer scan** — track relevant industry influencers on LinkedIn, analyze their recent posts, extract performing hooks/angles/topics.

All results merged, deduplicated, quality gated.

### Step 3: Ideation (weekly session)

**Skill:** `./skills/03-weekly-ideation`

Takes research output and generates a ranked batch of content ideas:

→ Quality gate: each idea scored against ICP relevance
→ ICP tier scoring: which buyer tier does this idea serve?
→ Pillar mapping: which content pillar does it trace to?
→ Sized to posting cadence

Output: Ranked idea batch ready for hook generation.

### Step 4: Hooks (per idea)

**Skill:** `./skills/04-hook-generator`

50 battle-tested hook templates organized by emotional trigger:
- **Desire** — what they want
- **Curiosity** — what they need to know
- **Fear** — what they're afraid of losing

Generates 20+ hook variations for each approved idea. You pick the strongest opening.

Informed by 366-post creator analysis (7 GTM creators, April 2026 — see `creator-benchmark.md`):
- Hidden truth / contrarian = 512 avg likes (highest ceiling)
- "The [X] of [Y]" anatomy = 371 avg likes
- Number-led = 261 avg likes (reliable workhorse, highest volume)
- Cliffhanger (trailing "…") = 237 avg likes (default pattern — 44% of all posts)
- No emojis in hooks — consistent across all 7 creators

### Step 5: Copy (per idea)

**Skill:** `./skills/05-copy-developer`

Takes approved hook + idea brief + voice profile → full draft in documented voice.

Writing rules (from 366-post analysis + ColdIQ methodology):
- One thought per line — no paragraph exceeds 2 lines
- Bold unicode headers for sections (𝗕𝗢𝗟𝗗 𝗧𝗘𝗫𝗧)
- Arrow bullets (→) for process/workflow steps
- Specific tool names — never "use an enrichment tool"
- Credibility in first 3 lines
- No emojis
- 800-1500 characters sweet spot (242 avg likes vs 130 for short, 194 for long)
- Image/carousel default (224 avg likes vs 150 text-only vs 147 video)
- Listicle structure dominant (83-90% of top 4 creators)
- Numbered items when listing playbooks/steps
- Parenthetical asides for personality and color
- Engagement tail: question + optional P.S.
- Comment-bait CTA ("comment X to get Y") for engagement spikes — use selectively

### Step 6: Grade + Refine (per draft)

**Skill:** `./skills/06-post-grader`

5-dimension rubric, scored out of 50:

| Dimension | Max Score | What It Measures |
|-----------|----------|-----------------|
| Hook strength | /10 | Would you stop scrolling? |
| Voice match | /10 | Does it sound like the person? |
| ICP relevance | /10 | Does the target buyer care? |
| Structure & retention | /10 | Does it retain through to the end? |
| Reward & CTA | /10 | Does it deliver and close well? |

**Below 38 = sent back to copy developer with specific fixes per failing dimension.**
No vague "make it better." Targeted rewrites only.

Max 2 rewrite loops. Still doesn't pass? Flagged for human review.

### Step 7: Deliver + Schedule

**Skill:** `./skills/07-deliver-schedule`

→ Approved posts packaged with copy + visual brief + scheduling notes
→ ClickUp for client handoff and approval
→ Taplio for LinkedIn scheduling and analytics
→ Performance data fed back into Claude for next cycle

---

## The Feedback Loop

After every production session, the system captures:

**Feedback capture (automatic):**
- What was produced
- What changed during review
- What was rejected and why
- Appended to `learning-log.md`

**Pattern recognition (every 5 sessions):**
- Skill: `./maintenance/pattern-recognition`
- Reads the full learning log
- Identifies: what consistently gets changed, which hook types get rewritten, where voice drift occurs
- Outputs recommended updates to client folder and skill files

**Content auditor (monthly):**
- Skill: `./maintenance/content-auditor`
- Full strategy audit: pillar relevance, voice freshness, performance patterns
- Outputs prioritized maintenance report with ranked fixes

**Foundation doc refresh (as needed):**
- Voice profile, ICP, content pillars, CTA templates are living documents
- When the client raises a round, shifts ICP, or enters a new market, foundation docs get updated
- The auditor flags when it's time

**System check (pre-production):**
- Skill: `./maintenance/system-check`
- Tests every live dependency: env vars, Apify actors, Reddit access, Fireflies, Gemini, Google Docs
- Pass/fail checklist: GO or NO-GO
- Takes 2 minutes. Prevents a run from failing halfway through.

---

## Repurposing

**Skill:** `./skills/08-repurpose`

One LinkedIn post that performed well = one validated idea.

Restructured into 5 platform-native formats:
1. X/Twitter thread
2. Email newsletter
3. SEO blog post
4. Short-form video script
5. Carousel slides

Each format is rebuilt for how people consume on that platform. Not reformatted. Restructured.

**Important:** Each format still needs a human pass for voice and platform fit. Repurposing is not copy-pasting.

---

## Multi-Client Operation

Switch clients by name. Same skills, different context.

```
# Production run for any client
→ Claude reads clients/{{client_a}}/content/*.md
→ All skills operate against that client's voice, ICP, pillars

# Switch to another client
→ Claude reads clients/{{client_b}}/content/*.md
→ Same skills, different context
```

Each client folder is a self-contained content brain. Better files = better output.

---

## Quick Plays

### Foundation → first post in 48h
Voice profile + ICP + pillars built on day 1. First batch of ideas generated day 2. Hook variations + full draft by end of day 2.

### Transcript → content pipeline
One 30-minute client call through Fireflies. Extract 3-5 content-worthy moments. Develop each into a full draft with hooks.

### Post grader feedback loop
Every post scored on 5 dimensions before it ships. Over time, the learning log shows exactly where each client's content breaks down.

### 6-source parallel research
One keyword triggers 6 research workers simultaneously. What used to take a strategist hours runs in minutes.

### Repurpose flywheel
One LinkedIn post that performed well becomes 5 platform-native pieces.

---

## Service Line: Content Engine as a Service

This system is a productized service offering:

1. **Onboarding (Day 1-2):** Run foundation build — voice profile, ICP, pillars, brand guidelines
2. **Weekly production:** Research → ideation → hooks → copy → grade → deliver
3. **Monthly maintenance:** Content audit, voice refresh, pillar review
4. **Quarterly strategy:** Full performance review, pillar evolution, ICP expansion

**Pricing model:** Per-person per-month. Each person gets their own voice profile and production cadence.

**Deliverables:** Graded, voice-matched LinkedIn posts + repurposed content across platforms. Performance data fed back into the system.


## Compound Learning

**Before each run:** Read `clients/{{client}}/debrief-log.md` if it exists. Apply lessons tagged for this skill. Check for patterns that should change your approach.

**After each run:** If the user provides feedback (corrections, preferences, "this worked" / "this didn't"), append to the learning log below. Format: `- [DATE] [CLIENT]: [lesson] [CONFIDENCE: HIGH/MED/LOW]`

**Pattern promotion:** When the same lesson appears 3+ times across different clients, move it to the skill's Context Dependencies section as a permanent rule.

### Learning Log

<!-- Lessons accumulate here over time. Each entry should be specific and actionable. -->
<!-- Example: - 2026-04-15 CLIENT_X: Local-language openers get 3x reply rate vs English for this ICP [CONFIDENCE: HIGH] -->
