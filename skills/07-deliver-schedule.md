---
name: deliver-schedule
description: Delivery and scheduling — ClickUp client handoff, Taplio LinkedIn scheduling, performance data feedback loop into Claude for next cycle.
version: 1.0.0
---

# Deliver + Schedule

## Purpose

Package approved posts for client handoff, schedule for publishing, and feed performance data back into the system for the next production cycle.

## When to Use

- Step 7 in the content pipeline (after posts pass the grader)
- When a batch of posts is approved and ready for scheduling

## Prerequisites

- Graded posts (38+/50 from post grader)
- Client's `brand-guidelines.md` (for visual brief specs)
- Access to ClickUp and Taplio

---

## Step 1: Package for Handoff

For each approved post, prepare a handoff package:

```
POST PACKAGE — {{post_number}}/{{batch_total}}

Title: {{topic}}
Pillar: {{content pillar}}
ICP Tier: {{target tier}}
Post Grade: {{score}}/50
Scheduled: {{date + time}}

COPY:
{{the full approved post text}}

VISUAL BRIEF:
Type: {{image / carousel / none}}
Description: {{what the visual should show}}
Text overlay: {{exact copy for the visual, if any}}
Reference: {{link to similar visual or style reference}}
Brand elements: {{colors, fonts, logo placement from brand-guidelines.md}}

SCHEDULING NOTES:
- Best time: {{recommended posting time}}
- Hashtags: {{if applicable, from brand guidelines}}
- First comment: {{prepared first comment if strategy calls for it}}
```

## Step 2: ClickUp Handoff

Move post packages to ClickUp for client review and approval:

1. Create task per post in the client's ClickUp content board
2. Attach: copy, visual brief, scheduling notes
3. Status: "Ready for Review"
4. Assign to client contact for approval

**ClickUp task structure:**
- Task name: `[{{date}}] {{post topic}}`
- Description: Full copy + visual brief
- Custom fields: Pillar, ICP Tier, Post Grade, Scheduled Date
- Checklist: Copy approved / Visual approved / Scheduled

## Step 3: Taplio Scheduling

Once client approves:

1. Queue post in Taplio at scheduled time
2. Set up: post text, image (if applicable), first comment (if applicable)
3. Verify preview renders correctly (line breaks, formatting)

**Scheduling guidelines:**
- Tuesday through Thursday = highest acceptance rates
- Avoid weekends and Mondays (20%+ drop in engagement)
- Morning posts (7:30-9:00 AM local time) for B2B audiences
- Space posts minimum 24 hours apart
- Never post during major industry events unless the post is about that event

## Step 4: Performance Data Feedback

After posts are published (typically 48-72 hours for LinkedIn engagement to settle):

1. Pull engagement data from Taplio analytics:
   - Impressions
   - Likes
   - Comments
   - Shares
   - Profile views driven
   - Click-through rate (if link in post)

2. Map performance back to post metadata:
   ```
   Post: "{{hook}}"
   Published: {{date}}
   Pillar: {{pillar}} | ICP Tier: {{tier}} | Post Type: {{archetype}}
   Hook template: #{{n}} | Post Grade: {{score}}/50

   Performance:
   - Impressions: {{n}}
   - Likes: {{n}}
   - Comments: {{n}}
   - Shares: {{n}}
   - Engagement rate: {{%}}
   ```

3. Feed into learning log:
   - Append performance data to `learning-log.md`
   - Flag top performers (top 20% by engagement) for repurposing
   - Flag underperformers (bottom 20%) for pattern analysis

4. Update system intelligence:
   - Which hook templates are performing best for this client?
   - Which content pillars drive the most engagement?
   - Which ICP tier responds most?
   - What word count range works best?
   - What posting times perform best?

---

## Monthly Performance Report

At end of each month, generate:

```
CONTENT PERFORMANCE — {{client_name}} — {{month}}

Posts published: {{n}}
Total impressions: {{n}}
Total engagement: {{likes + comments + shares}}
Avg engagement rate: {{%}}
Follower growth: {{start}} → {{end}} ({{+/- n}}, {{%}} growth)

Top 3 posts:
1. "{{hook}}" — {{engagement}} — {{why it worked}}
2. ...
3. ...

Bottom 3 posts:
1. "{{hook}}" — {{engagement}} — {{why it underperformed}}
2. ...
3. ...

Pillar performance:
| Pillar | Posts | Avg Engagement | Trend |
|--------|-------|----------------|-------|

Hook pattern performance:
| Pattern | Posts | Avg Engagement | Trend |
|---------|-------|----------------|-------|

Recommendations for next month:
- {{specific, data-backed recommendations}}
```
