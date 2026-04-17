---
name: research-workers
description: 6 parallel research workers — LinkedIn/Apify, Reddit, YouTube/Gemini, X/Twitter, Fireflies transcripts, repurposing archive. Plus weekly influencer scanning. Merged, deduplicated, quality gated.
version: 1.0.0
---

# Research Workers

## Purpose

Find what to write about and when. Six research workers fire in parallel, scan different sources, and return merged, deduplicated, quality-gated research — ready for the ideation session.

Plus: weekly influencer scan to track what's performing in the client's niche right now.

## When to Run

- Weekly, before the ideation session (Step 2 in pipeline)
- Ad-hoc when a specific topic or event needs rapid research
- Before onboarding a new client (initial landscape scan)

## Prerequisites

- Client's `icp.md` (for relevance filtering)
- Client's `content-pillars.md` (for topic alignment)
- Keywords and niche terms from client profile
- API access: Apify, Reddit, Fireflies (optional: Gemini, X API)

---

## The 6 Workers

### Worker 1: LinkedIn Trend Scraping (Apify)

**What it does:** Scrapes recent high-performing posts in the client's niche on LinkedIn.

**Apify Actor:** `harvestapi/linkedin-profile-posts` (ID: `A3cAPGpwBEG8RJwse`)
**API:** `https://api.apify.com/v2/acts/A3cAPGpwBEG8RJwse/runs`
**Auth:** Apify API token (env var or stored in `~/.apify/auth.json`)

**Baseline benchmark:** `creator-benchmark.md` — 366-post analysis of 7 top GTM creators (Michel Lieben, Alex Vacca, Fivos Aresti, Dan Rosenthal, Patrick Spychalski, Eric Nowoslawski, Alex Fine). Use as baseline for engagement scoring and pattern detection.

**How:**
1. Define target creators list (competitors, peers, aspirational accounts)
2. Run Apify actor with creator LinkedIn profile URLs:
   ```json
   {
     "profileUrls": ["https://www.linkedin.com/in/{{username}}/"],
     "maxPosts": 50,
     "scrapeReactions": false,
     "scrapeComments": false,
     "includeReposts": false,
     "includeQuotePosts": true
   }
   ```
   **Important:** Keep `scrapeReactions: false` — reactions bloat the dataset 100x and can cause run aborts.
3. Filter by engagement threshold (likes > 100 or comments > 20)
4. Extract: hook text, post structure, topic, word count, engagement metrics

**Output per post:**
```
Hook: "{{first line}}"
Topic: {{topic classification}}
Structure: {{list/steps/story/reasons}}
Engagement: {{likes}} / {{comments}} / {{shares}}
Word count: {{n}}
Angle: {{what makes this post work}}
Steal-worthy: {{specific element to adapt — hook pattern, structure, topic angle}}
```

**Weekly influencer scan addition:**
- Maintain a list of 15-25 industry influencers per client
- Track their posting patterns, topic shifts, engagement trends
- Flag: new topics gaining traction, formats outperforming, hooks worth adapting
- Output: "Influencer Intel Brief" — what the top voices in your niche talked about this week

### Worker 2: Reddit Mining

**What it does:** Surfaces real audience pain language from niche communities.

**How:**
1. Identify 5-10 relevant subreddits from `icp.md` buyer language
2. Search for posts with high engagement (upvotes > 50) in last 30 days
3. Mine comments for pain language, frustrations, questions
4. Extract verbatim phrases — the words real people use when they're frustrated

**Output:**
```
Subreddit: r/{{sub}}
Thread: "{{title}}"
Pain language found:
- "{{verbatim quote}}" ({{upvotes}} upvotes)
- "{{verbatim quote}}"
Content angle: {{how to turn this pain into a post}}
ICP tier match: {{Tier 1/2/3}}
```

**Why this matters:** Marketers write "optimize your pipeline." Buyers write "I'm drowning in leads that go nowhere." Reddit gives you the buyer's words.

### Worker 3: YouTube Mining (Gemini)

**What it does:** Extracts frameworks from long-form video content worth adapting to LinkedIn format.

**How:**
1. Search YouTube for recent videos (last 30 days) in client's niche
2. Filter by views > 5K and relevant channels
3. Use Gemini to analyze transcripts and extract:
   - Core frameworks or mental models presented
   - Data points or case studies mentioned
   - Contrarian takes or surprising claims
   - Structural patterns worth adapting

**Output:**
```
Video: "{{title}}" by {{creator}}
Views: {{n}} | Length: {{min}}
Framework: {{name/description}}
Key insight: "{{specific takeaway}}"
LinkedIn adaptation: {{how to restructure for a post}}
Pillar match: {{which content pillar}}
```

### Worker 4: X/Twitter Signal

**What it does:** Captures live debates, hot takes, and trending discussions in the industry.

**How:**
1. Search X for trending topics and debates in client's niche (last 7 days)
2. Filter for threads with high engagement (likes > 100, replies > 20)
3. Identify: what people are arguing about, POV opportunities, contrarian positions

**Output:**
```
Thread/Tweet: "{{text}}"
By: {{handle}} ({{followers}})
Engagement: {{likes}} / {{replies}} / {{retweets}}
Debate angle: {{the core disagreement}}
POV opportunity: {{client's potential take on this}}
Timeliness: {{how long this is relevant — days/weeks}}
```

### Worker 5: Fireflies Transcripts

**What it does:** Mines client call recordings for content gold. Highest-signal source in the system.

**How:**
1. Pull recent Fireflies transcripts (last 2-4 weeks)
2. Scan for content-worthy moments:
   - Real objections raised by prospects
   - Client wins or results shared on calls
   - Questions that keep coming up
   - Surprising insights or "aha moments"
   - Language the client uses naturally (voice profile fuel)

**Output:**
```
Call: {{meeting name}} — {{date}}
Content moment: "{{verbatim quote or paraphrase}}"
Why it's content: {{explanation}}
Post type: {{story / contrarian / playbook / case study}}
Hook draft: "{{rough hook based on this moment}}"
```

**Why this is the highest-signal source:** These are real conversations with real buyers about real problems. No guessing. No trend-chasing. Pure signal.

### Worker 6: Repurposing Archive

**What it does:** Analyzes the client's own post history — what worked, what didn't, what themes are overdue for a refresh.

**How:**
1. Pull client's LinkedIn post history (Taplio analytics or Apify scrape)
2. Rank by engagement: top 20%, bottom 20%
3. Analyze top performers: hook type, structure, topic, word count
4. Identify:
   - Winning topics/angles worth repeating (audiences don't remember individual posts)
   - Underperforming angles to drop or rethink
   - Content gaps — pillars that haven't been covered recently
   - Refresh opportunities — old posts with new data or updated takes

**Output:**
```
Top performing posts (last 90 days):
1. "{{hook}}" — {{likes}}/{{comments}} — Topic: {{topic}}
   Why it worked: {{analysis}}

Content gaps:
- Pillar "{{pillar}}" hasn't been covered in {{n}} weeks
- Topic "{{topic}}" performed well 60 days ago — due for refresh

Refresh candidates:
- "{{old post hook}}" → update with {{new data/angle}}
```

---

## Merge & Quality Gate

After all 6 workers return results:

### Step 1: Merge
Combine all research into a single document organized by content pillar.

### Step 2: Deduplicate
Remove overlapping insights across sources. If Reddit and Fireflies surface the same pain point, merge them (stronger signal).

### Step 3: Quality Gate

Score each research finding:

| Criteria | Weight |
|----------|--------|
| ICP relevance (matches documented pain) | 30% |
| Freshness (recency of the insight) | 20% |
| Signal strength (multiple sources confirm it) | 20% |
| Content potential (can this become a post?) | 15% |
| Pillar alignment (traces to a content pillar) | 15% |

**Gate:** Only findings scoring 60%+ pass to the ideation session.

### Step 4: Output
Deliver ranked research findings to the weekly ideation session as input.

---

## Influencer Scan Protocol

**Frequency:** Weekly (runs as part of Worker 1 but gets its own output section)

**Setup per client:**
1. Identify 15-25 influencers in their industry/niche
2. Categorize: Tier 1 (direct competitors), Tier 2 (adjacent voices), Tier 3 (aspirational)
3. Store list in `clients/{{client}}/content/influencer-list.md`

**Weekly scan outputs:**
```
INFLUENCER INTEL BRIEF — Week of {{date}}

Trending topics this week:
1. {{topic}} — covered by {{n}} influencers, avg engagement {{n}}
2. {{topic}} — breakout post by {{name}}, {{engagement}}

Hook patterns performing:
- {{pattern}} (used by {{names}}, avg {{engagement}})

New angles spotted:
- {{influencer}} posted about {{topic}} from {{unusual angle}}

Format trends:
- {{carousel/image/text-only}} outperforming this week

Gaps (nobody is talking about):
- {{topic your client could own}}
```

---

## Reverse Engineering (bonus worker)

When a specific high-performing post needs to be deconstructed:

1. Identify the post
2. Extract: hook type, structure, word count, formatting patterns
3. Map to hook template library (which of the 50 templates does it match?)
4. Identify the reusable framework vs the specific content
5. Output: template + brief for adapting to client's voice and topic
