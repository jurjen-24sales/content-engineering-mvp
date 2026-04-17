---
name: system-check
description: Pre-production dependency check. Tests every live dependency the engine uses. Pass/fail checklist. GO or NO-GO. Takes 2 minutes. Prevents a run from failing halfway through.
version: 1.0.0
---

# System Check

## Purpose

Before any production round, test every live dependency the engine uses. Pass/fail checklist. GO or NO-GO decision. Takes 2 minutes. Prevents a run from failing halfway through.

## When to Run

- Before every production session
- After any API key rotation or tool update
- When a production run failed mid-way (diagnose which dependency broke)

---

## Checklist

### Foundation Files

| Check | Status |
|-------|--------|
| `client-profile.md` exists and is populated | [ ] |
| `voice-profile.md` exists and is populated | [ ] |
| `icp.md` exists and has 3 tiers | [ ] |
| `content-pillars.md` exists and has 3+ pillars | [ ] |
| `cta-templates.md` exists | [ ] |
| `brand-guidelines.md` exists | [ ] |
| `influencer-list.md` exists and has ≥15 profiles with LinkedIn URLs | [ ] |
| `learning-log.md` exists | [ ] |
| `weekly-intel/` folder exists (auto-created on first run) | [ ] |

### API Dependencies

| Check | Status |
|-------|--------|
| Apify API key valid (test with simple actor run — `harvestapi/linkedin-profile-posts`) | [ ] |
| Apify actor `A3cAPGpwBEG8RJwse` reachable for weekly-influencer-analysis | [ ] |
| Reddit API access working | [ ] |
| Fireflies API access working (if using transcripts) | [ ] |
| Gemini API key valid (if using for images/YouTube) | [ ] |
| Google Docs API access (if using for output) | [ ] |

### External Tools

| Check | Status |
|-------|--------|
| ClickUp workspace accessible | [ ] |
| ClickUp content board exists for this client | [ ] |
| Taplio account connected | [ ] |
| Taplio can queue posts | [ ] |

### Environment

| Check | Status |
|-------|--------|
| All required env vars set | [ ] |
| Client folder path resolves correctly | [ ] |
| Influencer list last refreshed <90 days ago (quarterly refresh) | [ ] |
| `APIFY_TOKEN` env var set | [ ] |
| Previous session's learning log is up to date | [ ] |

---

## Decision Gate

| Result | Action |
|--------|--------|
| All checks pass | **GO** — proceed with production |
| Foundation files missing | **NO-GO** — run foundation build first |
| 1-2 API deps failing | **PARTIAL GO** — run without those workers, note in output |
| 3+ API deps failing | **NO-GO** — resolve API issues before proceeding |
| External tools failing | **GO with manual delivery** — produce content but deliver manually |

---

## Output Format

```
SYSTEM CHECK — {{client_name}} — {{date}}

Foundation files: {{n}}/7 OK
API dependencies: {{n}}/{{total}} OK
External tools: {{n}}/{{total}} OK
Environment: {{n}}/{{total}} OK

DECISION: {{GO / PARTIAL GO / NO-GO}}

{{If NO-GO or PARTIAL GO: list specific failures and resolution steps}}
```
