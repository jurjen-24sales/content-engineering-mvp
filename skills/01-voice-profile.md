---
name: voice-profile
description: 25-question voice DNA conversation that captures how someone actually talks — beliefs, humor, rhythm, hard NOs. Outputs voice-profile.md as the AI guardrail for every draft.
version: 1.0.0
---

# Voice Profile Builder

## Purpose

Run a 25-question conversation to extract someone's authentic voice. This is NOT a form. It's a real conversation that captures how they think, what they believe, and how they naturally communicate.

Without this, every post sounds like everyone else.

## When to Run

- First time onboarding a new content client
- Voice refresh (quarterly, or after major business change)
- When learning log shows consistent voice drift

## How It Works

**Format:** Conversational interview, not a questionnaire. Ask one question at a time. Let them talk. Follow up on interesting answers. The goal is to hear their natural speech patterns, not their prepared answers.

**Duration:** 30-45 minutes (can be done live or async over chat)

**Output:** `voice-profile.md` in the client's content folder

---

## The 25 Questions

### Block 1: Identity & Beliefs (Questions 1-7)

These establish who they are and what they stand for.

1. **What do you do, and how would you explain it to someone at a dinner party?**
   → Captures their natural elevator pitch, not the corporate version.

2. **What's the biggest misconception in your industry that makes you angry?**
   → Surfaces their contrarian takes — the beliefs that make their content distinct.

3. **What hill would you die on professionally?**
   → Non-negotiable belief. This becomes a recurring theme in their content.

4. **What advice do you hear repeated in your space that you think is wrong?**
   → More contrarian fuel. Content gold lives in disagreement.

5. **Who do you admire in your industry, and why?**
   → Reveals their values and the standard they hold themselves to.

6. **What's something you used to believe that you've completely changed your mind about?**
   → Shows intellectual honesty. Great for story-based content.

7. **If you could only teach one thing to your audience, what would it be?**
   → Their core message. Everything traces back to this.

### Block 2: Communication Style (Questions 8-14)

These capture HOW they talk, not just what they say.

8. **When you're explaining something complex, do you use analogies, data, stories, or something else?**
   → Identifies their default teaching mode.

9. **Read me the last three texts you sent to a colleague or friend.**
   → Real language, unfiltered. Best signal for actual voice.

10. **What words or phrases do you catch yourself repeating?**
    → Signature language that should appear in their content.

11. **Do you swear in professional settings? How casual are you?**
    → Calibrates the formality dial.

12. **How do you respond when someone disagrees with you publicly?**
    → Reveals their conflict style — important for contrarian content.

13. **What kind of humor do you use? Give me an example of something that made you laugh recently.**
    → Humor is the hardest thing for AI to replicate. Get specific examples.

14. **If your LinkedIn content was a TV show, what show would it be?**
    → Metaphor that captures their vibe instantly.

### Block 3: Audience & Content (Questions 15-20)

These calibrate their relationship with their audience.

15. **Who exactly are you writing for? Paint me a picture of that person.**
    → Their mental model of their reader. May differ from the formal ICP.

16. **What do you want people to feel after reading your content?**
    → Emotional target. Informed/inspired/challenged/seen/etc.

17. **What kind of content do YOU engage with? What makes you stop scrolling?**
    → What they consume shapes what they create.

18. **What's a post you've written that you're proud of? What made it work?**
    → Self-awareness about their own content. Pull specific examples.

19. **What's a post you've seen from someone else that you wished you'd written?**
    → Aspiration benchmark. Reveals the voice they're gravitating toward.

20. **What topics are off-limits? What would make you cringe if AI wrote it under your name?**
    → Hard NOs. Critical guardrails.

### Block 4: Stories & Experience (Questions 21-25)

These mine the raw material for content.

21. **What's the hardest professional lesson you've learned? Tell me the full story.**
    → Deep story content. Context → Problem → Action → Result.

22. **What happened in the last week that surprised you?**
    → Recent past content fuel. Fresh and relevant.

23. **What's something your clients keep asking you about?**
    → Demand signal. Write about what people already want to know.

24. **What's a win you had recently that you haven't told anyone about yet?**
    → Unpublished material. Original content that hasn't been done.

25. **What do you want to be known for in 3 years?**
    → Direction. Shapes pillar evolution and content trajectory.

---

## Processing the Conversation

After the conversation, build the voice profile:

### 1. Extract Voice DNA

From their answers, identify:
- **Sentence length patterns** — do they speak in short punches or longer flowing sentences?
- **Vocabulary level** — jargon-heavy, simple, mixed?
- **Default tone** — direct, warm, provocative, analytical, self-deprecating?
- **Humor style** — dry, sarcastic, self-deprecating, none?
- **Teaching mode** — analogies, data, stories, frameworks?
- **Formality level** — corporate, casual, somewhere between?

### 2. Build Guardrails

From questions 3, 4, 12, 20:
- **Hard NOs** — phrases, tones, or approaches they reject
- **Beliefs** — non-negotiable positions that recur in content
- **Conflict style** — how they handle disagreement (important for contrarian posts)

### 3. Pull Sample Snippets

From questions 9, 10, 18, 21:
- Extract 5-10 sentences that are peak "them"
- These become the reference for voice-matching in the copy developer

### 4. Map to Writing Rules

Translate voice DNA into concrete DO/DON'T rules:
- "Opens with direct statement, never a question"
- "Uses 'look' and 'here's the thing' as transitions"
- "Never uses emojis or exclamation marks"
- "Drops in personal anecdotes mid-argument"

### 5. Save to Client Folder

Write the completed `voice-profile.md` to `clients/{{client}}/content/voice-profile.md` using the template structure.

---

## Voice Refresh Protocol

Run when:
- Learning log shows 3+ sessions with voice drift notes
- Content auditor flags voice staleness
- Client has had a major business change (new role, new market, funding, etc.)

Refresh process:
1. Pull 3-5 recent Fireflies transcripts
2. Compare speech patterns against existing voice profile
3. Run 5-question mini-interview (questions 2, 9, 10, 20, 23)
4. Update voice-profile.md with changes logged in the refresh table
