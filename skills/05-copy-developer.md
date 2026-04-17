---
name: copy-developer
description: Takes approved hook + idea brief + voice profile and writes a full LinkedIn draft in the client's documented voice. Not generic AI copy.
version: 1.0.0
---

# Copy Developer

## Purpose

Write a full LinkedIn draft in the client's documented voice. Takes the approved hook from the hook generator, the idea brief from the ideation session, and the voice profile — and produces a post that sounds like the actual person wrote it.

## When to Use

- Step 5 in the content pipeline (after hooks, before post grader)
- When rewriting a draft flagged by the post grader (with specific fix instructions)
- When adapting a repurposed piece for LinkedIn format

## Prerequisites

**Required inputs:**
- Approved hook (from hook generator, step 4)
- Idea brief (from ideation session, step 3)
- `voice-profile.md` (guardrail for the entire draft)
- `icp.md` (to speak to the right buyer)
- `content-pillars.md` (strategic alignment)
- `cta-templates.md` (for the engagement tail)
- `brand-guidelines.md` (formatting preferences)

**Optional:**
- Post grader feedback (if this is a rewrite loop)
- Reference posts (high-performing examples in similar format)

---

## Writing Process

### Step 1: Load Voice Guardrails

Before writing a single word, read and internalize:
- Voice DNA: sentence length, vocabulary, tone, humor style
- Hard NOs: phrases, approaches, topics to avoid
- Sample snippets: 5-10 sentences that are peak "them"
- Writing rules: specific DO/DON'T from the voice profile

**If the voice profile doesn't exist, STOP. Run the voice profile skill first.**

### Step 2: Map Structure

Based on the idea brief and post type, choose the retention structure:

| Post Type | Primary Structure | Secondary |
|-----------|------------------|-----------|
| Playbook/Process | Numbered stages + arrow bullets | Story setup |
| Listicle | Numbered items with 2-3 line explanations | Parenthetical asides |
| Contrarian Take | Problem → flip → evidence → implication | Bold claim hook |
| Behind-the-Scenes | Story → process reveal → tools named | Result number |
| Case Study | Context → problem → solution → numbers | Specific tools |
| Tool Stack | Categorized list with 1-line descriptions | Section headers |
| Story | Context → Problem → Action → Result | Lesson/insight |

### Step 3: Write the Draft

**LinkedIn formatting rules (non-negotiable):**

1. **One thought per line.** No paragraph exceeds 2 lines. Every distinct thought gets its own line break. White space is a feature.

2. **Bold unicode headers for sections.** Use 𝗕𝗢𝗟𝗗 𝗧𝗘𝗫𝗧 for section headers when the post has 3+ sections.
   - Generate using unicode bold: 𝗔𝗕𝗖𝗗𝗘𝗙𝗚𝗛𝗜𝗝𝗞𝗟𝗠𝗡𝗢𝗣𝗤𝗥𝗦𝗧𝗨𝗩𝗪𝗫𝗬𝗭 𝗮𝗯𝗰𝗱𝗲𝗳𝗴𝗵𝗶𝗷𝗸𝗹𝗺𝗻𝗼𝗽𝗾𝗿𝘀𝘁𝘂𝘃𝘄𝘅𝘆𝘇

3. **Arrow bullets (→) for process/workflow steps.** Not for everything — only when showing a sequence or how-to.

4. **Numbered items** for lists, playbooks, or ranked items.

5. **Specific tool names.** Never "use an enrichment tool." Name it: "Run a waterfall in Clay: Wiza → Prospeo → LeadMagic → FullEnrich."

6. **Credibility in first 3 lines.** A number, result, or experience proof. The reader decides in the first scroll whether you've earned the right to teach them.

7. **No emojis.** Period. Consistent across all 7 top GTM creators analyzed (366 posts). They cheapen the content.

8. **800-1500 characters (roughly 150-280 words).** Sweet spot from 366-post analysis: medium-length posts average 242 likes vs 130 for short (<800 chars) and 194 for long (1500+ chars). Up to 2000+ chars for playbook/process posts only.

8a. **Image/carousel > text-only > video for likes.** Images average 224 likes vs 150 text-only vs 147 video. Default to image/carousel unless the idea specifically calls for video or pure text.

9. **Parenthetical asides for personality.** "(Most teams ignore this. Expensive lesson.)" — adds human color without breaking structure.

10. **Strong closer.** Not a generic sign-off. Either a punchy one-liner, a callback to the opening, or a direct statement.

11. **Engagement tail.** Every post ends with:
    - A question (drives comments) — OR
    - A question + P.S. (question + soft CTA)
    - Match CTA type to post type from `cta-templates.md`

### Step 4: Voice Check

Before submitting to the post grader, run a self-check:

- [ ] Read the draft out loud — does it sound like the person?
- [ ] Check against 3 sample snippets from voice profile — same rhythm?
- [ ] Scan for hard NO violations — any phrases they'd cringe at?
- [ ] Verify formality level matches voice profile
- [ ] Check humor (if applicable) matches their style
- [ ] Confirm no generic AI phrases: "In today's fast-paced world," "Let me share," "I'm excited to announce"

### Step 5: Submit for Grading

Send the completed draft to the post grader (step 6 in pipeline).

---

## Rewrite Protocol

When the post grader returns a draft with a score below 38/50:

1. **Read the specific fix instructions** per failing dimension
2. **Only fix what's flagged.** Don't rewrite the entire post — targeted fixes only.
3. **Re-check voice match** after fixes (rewrites often drift)
4. **Resubmit** to the post grader

Max 2 rewrite loops. After loop 2, if still below 38: flag for human review with a note on what's not working.

---

## Output Format

```
DRAFT: {{post title/topic}}
Post type: {{archetype}}
Word count: {{n}}
ICP tier: {{primary tier}}
Pillar: {{content pillar}}
Hook template: #{{n}} from hook generator

---

{{The full LinkedIn post draft}}

---

VOICE CHECK:
- Rhythm match: {{yes/no + note}}
- Hard NO violations: {{none / list}}
- Formality level: {{matches / too formal / too casual}}
- AI phrase scan: {{clean / flagged phrases}}
```

---

## Copy Anti-Patterns

- **Don't start writing without reading the voice profile.** The voice profile IS the skill. Without it, you're just generating generic LinkedIn content.
- **Don't frontload the product/service.** Product mentions land in the last 20% of the post, never the first 50%.
- **Don't use filler.** Every line must add value. If you can remove a sentence and lose nothing, remove it.
- **Don't format DMs like blog posts.** If this is a DM draft (not a post), no bold, no bullets, no formatting. Real humans don't format LinkedIn messages.
- **Don't write "How to" when you mean "How I."** Share experience, not prescriptions. No one can question your lived experience.
- **Don't hedge.** "I think maybe" → "Here's what I've seen." Confidence without arrogance.
