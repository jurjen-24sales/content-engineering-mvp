---
name: pattern-recognition
description: Reads the full learning log across sessions. Identifies what consistently gets changed, which hook types get rewritten, where voice drift occurs. Outputs recommended updates to client folder and skill files. Run every 5 sessions.
version: 1.0.0
---

# Pattern Recognition

## Purpose

Read the full learning log and identify patterns that inform system updates. What consistently gets changed? Which hook types get rewritten? Where is voice drifting? Turn session noise into system upgrades.

## When to Run

- Every 5 production sessions (automatic trigger)
- When content auditor flags performance issues
- Before a voice refresh (to identify what's drifting)

## Prerequisites

- Client's `learning-log.md` (minimum 5 sessions of data)
- Client's `voice-profile.md` (current version)
- Client's `content-pillars.md`
- Performance data from deliver-schedule (if available)

---

## Analysis Framework

### 1. Rewrite Pattern Analysis

Scan the learning log for:
- **Hook rewrites:** Which hook templates consistently score below 7/10?
- **Voice corrections:** Which phrases or patterns keep getting flagged?
- **Structure issues:** Which post types consistently need restructuring?
- **CTA mismatches:** Which CTA types keep getting changed?

Output:
```
REWRITE PATTERNS (last {{n}} sessions):

Hooks rewritten: {{n}}/{{total}} ({{%}})
Most rewritten hook types: {{list}}
Recommendation: {{update hook generator to deprioritize/modify these templates}}

Voice corrections: {{n}} instances
Recurring drift: {{specific patterns — e.g., "too formal," "missing humor," "using banned phrases"}}
Recommendation: {{update voice profile with stronger guardrails on {{specific areas}}}}

Structure rewrites: {{n}}/{{total}}
Common issue: {{e.g., "posts over 300 words consistently need trimming"}}
Recommendation: {{update copy developer with tighter word count constraint}}
```

### 2. Performance Correlation

If performance data is available, correlate:
- Post grade vs actual engagement (does the grader predict performance?)
- Hook type vs engagement (which hooks actually perform for THIS client?)
- Pillar vs engagement (which topics resonate?)
- Word count vs engagement (what's the client-specific sweet spot?)
- Posting time vs engagement

Output:
```
PERFORMANCE CORRELATIONS:

Grader accuracy: {{correlation between grade and engagement}}
Best-performing hook type: {{type}} ({{avg engagement}})
Best-performing pillar: {{pillar}} ({{avg engagement}})
Client-specific word count sweet spot: {{range}}
Best posting time: {{day/time}}
```

### 3. Voice Drift Detection

Compare recent session outputs against voice profile:
- Are sample snippets still representative?
- Has the client's natural language evolved?
- Are hard NOs being respected or eroded?

Output:
```
VOICE DRIFT ASSESSMENT:

Drift detected: {{yes/no}}
Drift direction: {{e.g., "more formal over time," "losing humor," "more jargon"}}
Sessions since last voice refresh: {{n}}
Recommendation: {{schedule voice refresh / update specific guardrails / no action needed}}
```

### 4. System Recommendations

Based on all analysis, output ranked recommendations:

```
RECOMMENDED UPDATES (ranked by impact):

1. [HIGH] {{recommendation}} — {{reason from data}}
   Action: {{specific file to update and what to change}}

2. [MEDIUM] {{recommendation}} — {{reason}}
   Action: {{specific change}}

3. [LOW] {{recommendation}} — {{reason}}
   Action: {{specific change}}
```
