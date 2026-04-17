---
name: post-grader
description: 5-dimension content grading rubric, /50 score. Below 38 triggers targeted rewrites. No vague feedback. Max 2 loops then human review.
version: 1.0.0
---

# Post Grader

## Purpose

Score every draft across 5 dimensions before it ships. Total out of 50. Below 38 = sent back to copy developer with specific fixes per failing dimension. No vague "make it better."

## When to Use

- After every draft from the copy developer (Step 6 in pipeline)
- When reviewing existing content for quality
- During content audits to benchmark historical performance

## Prerequisites

Must have access to:
- The client's `voice-profile.md` (for voice match scoring)
- The client's `icp.md` (for ICP relevance scoring)
- The client's `content-pillars.md` (for strategic alignment)
- The draft to be graded

---

## The 5 Dimensions

### Dimension 1: Hook Strength (/10)

Does the first line make you stop scrolling?

| Score | Criteria |
|-------|----------|
| 9-10 | Specific number OR bold contrarian claim. Credibility proof in first 3 lines. Would stop a busy VP mid-scroll. |
| 7-8 | Strong opening with clear value promise. Missing either specificity or credibility. |
| 5-6 | Decent hook but generic. Could be anyone's post. No unique angle. |
| 3-4 | Weak opener. Starts with "I'm excited to announce" or vague thought leadership. |
| 1-2 | No hook. Opens with context nobody asked for. |

**Scoring inputs (from 366-post creator analysis — see `creator-benchmark.md`):**
- Hidden truth / contrarian = 512 avg likes (highest ceiling)
- "The [X] of [Y]" anatomy = 371 avg likes
- Number-led = 261 avg likes (reliable workhorse)
- Cliffhanger trailing "…" = 237 avg likes (default pattern, 44% of posts)
- Builder/Maker = 228 avg likes
- Questions = 161 avg likes (drives comments, inconsistent for likes)
- Explainer "Here's how/why" = 119 avg likes (lowest — avoid as primary hook)
- No emojis in hooks — consistent across all 7 top creators (penalize)
- "I'm excited to announce" = immediate -3 penalty
- **Engagement benchmarks:** Good = 150+ likes, Strong = 300+, Viral = 600+

**Fix template:** "Hook scores {{score}}/10. Problem: {{specific issue}}. Rewrite using {{recommended hook pattern}} with {{specific credibility proof or number from the brief}}."

### Dimension 2: Voice Match (/10)

Does it sound like the actual person, not generic AI?

| Score | Criteria |
|-------|----------|
| 9-10 | Reads like something they'd actually say. Matches sentence rhythm, vocabulary, humor, beliefs from voice profile. Could fool someone who knows them. |
| 7-8 | Mostly on-voice. Minor deviations — a phrase they wouldn't use, slightly too formal/casual. |
| 5-6 | Generic but not offensive. Doesn't violate hard NOs but doesn't sound like anyone specific. |
| 3-4 | Clearly AI-generated tone. Overly polished, uses phrases from their hard NO list. |
| 1-2 | Completely off-voice. Wrong tone, wrong vocabulary, wrong beliefs. |

**Scoring method:**
1. Compare draft against `voice-profile.md` sample snippets
2. Check for hard NO violations
3. Verify signature phrases are present where natural
4. Check formality level matches
5. Verify humor style (if applicable)

**Fix template:** "Voice scores {{score}}/10. Problems: {{list specific mismatches}}. The voice profile says '{{relevant guardrail}}' but the draft {{specific violation}}. Rewrite these sections: {{line references}}."

### Dimension 3: ICP Relevance (/10)

Does the target buyer actually care about this?

| Score | Criteria |
|-------|----------|
| 9-10 | Directly addresses a documented pain point for Tier 1 or Tier 2 buyer. Uses their language, not marketer language. They'd forward this to a colleague. |
| 7-8 | Relevant to ICP but slightly generic. Could be more specific to their situation. |
| 5-6 | Tangentially relevant. Industry-adjacent but doesn't hit a specific pain point. |
| 3-4 | Wrong tier targeting. Writing for practitioners when pillars say decision-makers. |
| 1-2 | Irrelevant to ICP. Self-serving content that only the poster would care about. |

**Scoring method:**
1. Match post topic against `icp.md` pain points
2. Check language against ICP's search language (their words, not yours)
3. Verify which buyer tier is being addressed
4. Check against content pillar goals and funnel stage

**Fix template:** "ICP relevance scores {{score}}/10. This post targets {{identified tier}} but the pain point '{{stated pain}}' doesn't match documented pains. Reframe using: '{{specific pain language from icp.md}}'."

### Dimension 4: Structure & Retention (/10)

Does it retain attention through to the end?

| Score | Criteria |
|-------|----------|
| 9-10 | Unresolved questions pull you through. Clear structure (list/steps/story/reasons). One thought per line. White space. Interweaving. Value per second. |
| 7-8 | Good structure, minor pacing issues. A section drags or a transition is weak. |
| 5-6 | Structure exists but predictable. No momentum. Reader could stop mid-post without curiosity pulling them forward. |
| 3-4 | Dense paragraphs. No clear structure. Wall of text. |
| 1-2 | Unreadable formatting. No line breaks. No logical flow. |

**Scoring checklist:**
- [ ] One thought per line (no paragraph > 2 lines)
- [ ] Bold unicode headers for sections (if post has 3+ sections)
- [ ] Arrow bullets (→) for process steps
- [ ] Numbered items for lists/playbooks
- [ ] Parenthetical asides for personality
- [ ] Content length in 800-1500 chars range (sweet spot: 242 avg likes vs 130 short, 194 long)
- [ ] No emoji clutter
- [ ] Retention mechanism clear (list/steps/story/reasons)

**Fix template:** "Structure scores {{score}}/10. Issues: {{specific formatting/pacing problems}}. Fix: {{break up paragraph at line X}}, {{add transition between sections Y and Z}}, {{restructure as {{list/steps/story}} instead of current format}}."

### Dimension 5: Reward & CTA (/10)

Does it deliver on the hook's promise and close well?

| Score | Criteria |
|-------|----------|
| 9-10 | Fully delivers on hook promise. Reader walks away with actionable value. CTA matches post energy. Engagement tail drives comments. |
| 7-8 | Delivers but slightly under-promises. CTA present but could be stronger. |
| 5-6 | Partial delivery. Hook promised X, post delivered 70% of X. CTA feels bolted on. |
| 3-4 | Under-delivers. Hook promised 7 things, gave 4. Or all surface-level. |
| 1-2 | Clickbait. Hook promised something the post doesn't contain. No CTA. |

**Scoring method:**
1. Compare hook promise vs actual content delivered
2. Check CTA type matches post type (from `cta-templates.md`)
3. Verify engagement tail exists (question and/or P.S.)
4. Confirm no hard-selling in first 50% of post

**Fix template:** "Reward scores {{score}}/10. The hook promises '{{hook promise}}' but the post {{specific gap}}. Add: {{specific content to fill the gap}}. CTA issue: {{specific CTA problem and recommended fix}}."

---

## Scoring Process

### Step 1: Read prerequisites
Load `voice-profile.md`, `icp.md`, `content-pillars.md`, `cta-templates.md` from client folder.

### Step 2: Score each dimension
Score independently. Don't let a strong hook inflate the structure score.

### Step 3: Calculate total
Sum all 5 dimensions. Max = 50.

### Step 4: Decision gate

| Total Score | Action |
|------------|--------|
| 43-50 | Ship. Flag as potential top performer for repurposing. |
| 38-42 | Ship with minor tweaks (note them, don't loop back). |
| 30-37 | **Rewrite.** Send back to copy developer with specific fixes per dimension. Loop 1. |
| Below 30 | **Rewrite.** Major issues. Send back with full rewrite brief. Loop 1. |

### Step 5: Rewrite loop (if needed)
- Max 2 loops through copy developer
- Each loop includes specific fix instructions per failing dimension
- After loop 2, if still below 38: flag for human review with full scoring breakdown

### Step 6: Log results
Append to `learning-log.md`:
- Post topic, hook type, total score, dimension breakdown
- Whether it passed first time or needed loops
- What specifically was fixed

---

## Output Format

```
POST GRADE: {{title/topic}}

Hook Strength:        {{score}}/10  {{one-line note}}
Voice Match:          {{score}}/10  {{one-line note}}
ICP Relevance:        {{score}}/10  {{one-line note}}
Structure & Retention:{{score}}/10  {{one-line note}}
Reward & CTA:         {{score}}/10  {{one-line note}}
─────────────────────────────────
TOTAL:                {{score}}/50

VERDICT: {{SHIP / SHIP WITH TWEAKS / REWRITE / HUMAN REVIEW}}

{{If rewrite: specific fix instructions per failing dimension}}
```

---

## Grading Anti-Patterns

- **Never give vague feedback.** "Make it better" is not a fix. "Hook scores 4/10 because it opens with a question instead of a credibility number — rewrite using the result-lead pattern with the $153K MRR data point" is a fix.
- **Never inflate scores to avoid a loop.** The loop exists to catch bad content before it ships. A 35 is a 35.
- **Never score voice match without reading the voice profile.** If the voice profile doesn't exist, score 0/10 and flag.
- **Never let one strong dimension carry a weak post.** A 10/10 hook with 3/10 structure still needs a rewrite.
