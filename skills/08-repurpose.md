---
name: repurpose
description: One LinkedIn post that performed well = one validated idea. Restructured into 5 platform-native formats — X thread, newsletter, blog, video script, carousel. Restructured, not reformatted.
version: 1.0.0
---

# Repurpose

## Purpose

Take one LinkedIn post that performed well and restructure it into 5 platform-native formats. Each format is rebuilt for how people consume on that platform. Not reformatted. Restructured.

**Important:** Each format still needs a human pass for voice and platform fit. Repurposing is not copy-pasting.

## When to Use

- After performance data shows a post in the top 20% by engagement
- When building a content flywheel (one idea, many touchpoints)
- During content calendar planning to maximize proven ideas

## Prerequisites

- A LinkedIn post that performed well (flagged by deliver-schedule skill)
- Client's `voice-profile.md`
- Client's `brand-guidelines.md`

---

## The 5 Formats

### Format 1: X/Twitter Thread

**How people consume on X:** Fast scrolling, punchy takes, each tweet must stand alone but build on the previous one. Threads are consumed in 15-30 second chunks.

**Restructuring rules:**
- Tweet 1 = hook (adapted from LinkedIn hook, shorter — under 280 chars)
- Each subsequent tweet = one standalone insight from the post
- Arrow bullets become individual tweets
- Remove bold unicode headers (not native to X)
- Add numbering: "1/" "2/" etc.
- Last tweet = CTA or callback to tweet 1
- 5-12 tweets total (sweet spot for threads)
- No hashtags in tweets (X culture)

### Format 2: Email Newsletter

**How people consume email:** Dedicated reading time, longer attention span, personal connection. They opted in — they want depth.

**Restructuring rules:**
- Subject line = adapted from the LinkedIn hook (but email-native: shorter, curiosity-driven)
- Opening = personal context or story that the LinkedIn post compressed
- Body = expand on the key insight with MORE depth (not less)
- Add: data points, examples, case studies that didn't fit in the LinkedIn post
- Close = one clear CTA (reply, click, or forward)
- 400-800 words (email readers tolerate more than LinkedIn)
- Conversational tone, first-person, as if writing to one person

### Format 3: SEO Blog Post

**How people consume blogs:** Searching for answers, scanning headers, looking for comprehensive coverage. They arrived from Google with a specific question.

**Restructuring rules:**
- Title = SEO-optimized version of the LinkedIn hook (include target keyword)
- H2 headers for each major section
- Expand each section with how-to depth
- Add: screenshots, tool links, step-by-step instructions
- Include internal links to related posts
- Close with summary + CTA
- 1,200-2,000 words (SEO depth)
- Add meta description adapted from the hook

### Format 4: Short-Form Video Script

**How people consume short video:** Visual, fast, personality-driven. They're swiping through Reels/TikTok/Shorts. Hook in first 2 seconds.

**Restructuring rules:**
- Opening line = verbal version of the hook (spoken, not written)
- Script structure: Hook (2 sec) → Context (5 sec) → 3-5 key points (30-45 sec) → Punchline/CTA (5 sec)
- Total: 45-90 seconds
- Write for speaking rhythm, not reading rhythm
- Include visual cues: [show screen], [cut to B-roll], [text overlay]
- Close with a question or bold statement (drives comments)
- No arrow bullets or formatting — this is spoken word

### Format 5: Carousel Slides

**How people consume carousels:** Swiping through slides, one idea per slide, visual learning. High save rate on LinkedIn and Instagram.

**Restructuring rules:**
- Slide 1 = hook slide (big text, minimal design)
- Each subsequent slide = one key point from the post
- One idea per slide, max 25 words per slide
- Arrow bullets become individual slides
- Second-to-last slide = summary or key takeaway
- Last slide = CTA + profile tag
- 7-12 slides total
- Include visual brief for designer (from brand-guidelines.md)
- Typography-driven design (text-heavy carousels outperform image-heavy)

---

## Repurpose Process

### Step 1: Deconstruct the Original

From the performing LinkedIn post, extract:
- Core insight (the ONE thing the post teaches)
- Supporting points (the evidence/examples/steps)
- Hook angle (what made people stop scrolling)
- Voice elements (phrases, humor, personality moments)

### Step 2: Platform Mapping

For each format, ask:
- What's the consumption context? (scrolling feed vs dedicated reading vs searching)
- What depth does this platform expect? (punchy vs comprehensive)
- What formatting is native? (threads vs headers vs slides)
- What's the CTA opportunity? (reply vs click vs save vs follow)

### Step 3: Restructure (not reformat)

For each format:
1. Start from the core insight, not the LinkedIn text
2. Rebuild the structure for the platform's consumption pattern
3. Adjust depth: compress for X, expand for blog/newsletter
4. Adapt voice: same person, different context (you talk differently on stage vs in a DM)
5. Native formatting only (no LinkedIn formatting on X, no blog formatting in video)

### Step 4: Quality Check

For each repurposed piece:
- [ ] Does it stand alone? (someone who never saw the LinkedIn post should get full value)
- [ ] Is it platform-native? (would a regular user of this platform recognize this as belonging here?)
- [ ] Does it still sound like the person? (voice match)
- [ ] Is the CTA appropriate for the platform?

---

## Output Format

```
REPURPOSE PACKAGE — "{{original LinkedIn hook}}"
Original performance: {{likes}}/{{comments}}/{{shares}}
Core insight: {{one sentence}}

FORMAT 1: X/TWITTER THREAD
{{full thread, numbered tweets}}

FORMAT 2: EMAIL NEWSLETTER
Subject: {{subject line}}
{{full newsletter draft}}

FORMAT 3: SEO BLOG POST
Title: {{SEO title}}
Target keyword: {{keyword}}
{{full blog draft or detailed outline with key points per section}}

FORMAT 4: VIDEO SCRIPT
Duration: {{seconds}}
{{full script with visual cues}}

FORMAT 5: CAROUSEL SLIDES
Slides: {{n}}
{{slide-by-slide content + visual brief}}

HUMAN REVIEW NOTES:
- {{any platform-specific nuances that need a human eye}}
- {{voice elements that may need adjustment}}
```
