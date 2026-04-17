# Content Engineering MVP

> Full content production engine for Claude Code. Foundation → Research → Ideation → Hooks → Copy → Grade → Deliver. Multi-client, voice-matched, data-backed.

One terminal. One engine. Many people. Each person sounds like themselves at scale.

This is a **Claude Code skill system** — a chained set of prompts, templates, and methodology docs that turn a single terminal into a full content production pipeline. It was extracted from a working GTM agency workflow and genericized. No client data, no operator branding — just the engine.

---

## What this is

A 7-step LinkedIn content pipeline, plus maintenance and repurposing:

```
Foundation → Research → Ideation → Hooks → Copy → Grade → Deliver
   (once)     (weekly)    (weekly)  (per idea) (per idea) (per draft) (per batch)
```

Each step is a separate Claude Code skill. The orchestrator (`SKILL.md` at root) chains them together. Each client lives in `clients/{{client_name}}/content/` with their own voice profile, ICP, pillars, CTAs, and learning log.

Opinionated, not generic:

- **Voice-first.** Nothing ships until a 25-question voice interview is done. Without a voice profile, output sounds like AI.
- **Research before ideation.** Six parallel workers (LinkedIn scraping, Reddit mining, YouTube, X, call transcripts, repurposing archive) gather signal before a single idea is generated.
- **Hook + Copy are separate steps.** Hooks are generated from a 50-template library grouped by emotional trigger (desire / curiosity / fear), informed by a 366-post creator benchmark. Copy development happens against the approved hook.
- **Every draft is graded on 5 dimensions.** Below 38/50 gets auto-rewritten with dimension-specific fixes. Max 2 rewrite loops.
- **Repurpose is restructuring, not reformatting.** One validated LinkedIn post becomes 5 platform-native pieces — X thread, newsletter, SEO blog, short-form video script, carousel.
- **Learning log per client.** Every correction is captured. Patterns across 5+ sessions promote into permanent skill rules.

---

## Repo layout

```
.
├── SKILL.md                              # Orchestrator — chains all sub-skills
├── creator-benchmark.md                  # 366-post LinkedIn analysis (7 GTM creators)
├── skills/
│   ├── 01-voice-profile.md               # 25-question voice interview → voice profile + ICP + pillars + CTAs + brand
│   ├── 02-research-workers.md            # 6 parallel research workers + weekly influencer scan
│   ├── 03-weekly-ideation.md             # Ranked idea batch from research output
│   ├── 04-hook-generator.md              # 50 hook templates × emotional triggers × creator benchmark
│   ├── 05-copy-developer.md              # Approved hook + voice profile → full draft
│   ├── 06-post-grader.md                 # 5-dimension rubric, /50, auto-rewrite on fail
│   ├── 07-deliver-schedule.md            # ClickUp handoff + Taplio scheduling + performance loop
│   └── 08-repurpose.md                   # 1 post → 5 platform-native formats
├── maintenance/
│   ├── system-check.md                   # Pre-production GO/NO-GO (deps, APIs, env)
│   ├── pattern-recognition.md            # Every 5 sessions, reads learning log, flags drift
│   └── content-auditor.md                # Monthly strategy audit (pillars, voice, performance)
├── templates/
│   └── client-folder-template/           # Copy this for each new person/client
│       ├── client-profile.md
│       ├── voice-profile.md
│       ├── icp.md
│       ├── content-pillars.md
│       ├── cta-templates.md
│       ├── brand-guidelines.md
│       ├── learning-log.md
│       └── transcripts/
├── knowledge_base/
│   ├── methodology/
│   │   ├── content-unit-framework.md     # Hook + Retain + Reward
│   │   ├── content-scaling-strategy.md   # Depth-then-width scaling
│   │   └── hormozi-content-structure-formula.md  # 4-part content formula
│   └── business/
│       └── audience-as-compounding-asset.md      # Why audience is a compounding asset
└── docs/
    └── QUICKSTART.md                     # 5-minute install + first-run walkthrough
```

---

## Install

This is a Claude Code skill system. Clone into your `.claude/skills/` directory (or wherever your skill library lives):

```bash
# Global install (all projects)
cd ~/.claude/skills/
git clone https://github.com/jurjen-24sales/content-engineering-mvp.git content-engine

# OR project-specific install
cd <your-project>/.claude/skills/
git clone https://github.com/jurjen-24sales/content-engineering-mvp.git content-engine
```

Restart Claude Code (or run `/skills refresh` if your version supports it) — the `content-engine` skill should now be invokable.

**Requires:** Claude Code ([install guide](https://docs.anthropic.com/claude/docs/claude-code))

---

## First run

**See [`docs/QUICKSTART.md`](docs/QUICKSTART.md) for a full walkthrough.** TL;DR:

1. **Create a client folder.** Copy `templates/client-folder-template/` to `clients/<name>/content/`.
2. **Run the voice interview.** Invoke `./skills/01-voice-profile.md` — it runs a 25-question conversation and writes your voice profile, ICP, pillars, CTAs, and brand guidelines.
3. **Run weekly research.** Invoke `./skills/02-research-workers.md`. This fires six parallel workers + an influencer scan and outputs a deduplicated signal report.
4. **Generate ideas → hooks → copy → grade.** The orchestrator (`SKILL.md`) chains steps 3-6. Drafts below 38/50 get auto-rewritten.
5. **Deliver.** Approved drafts exit via `./skills/07-deliver-schedule.md` (ClickUp handoff + Taplio scheduling).

Optional but recommended: run `./maintenance/system-check.md` before every production session (2 minutes, catches missing API keys / broken dependencies before you waste a run).

---

## External tools this system assumes access to

The pipeline references external services. You don't need all of them — missing ones degrade gracefully (that worker just no-ops), but the more you plug in, the stronger the signal:

| Tool | Used for | Required? |
|---|---|---|
| Claude Code | Running the skills | **Yes** |
| Apify (harvestapi/linkedin-profile-posts) | LinkedIn scraping (Worker 1, Influencer Scan) | Strongly recommended |
| Reddit API | Audience pain mining (Worker 2) | Optional |
| Gemini API | YouTube long-form mining (Worker 3) | Optional |
| X / Twitter API | Live debate signal (Worker 4) | Optional |
| Fireflies.ai | Client call transcripts → content gold (Worker 5) | Strongly recommended |
| ClickUp | Client approval + handoff (Step 7) | Optional (can be replaced) |
| Taplio | LinkedIn scheduling + analytics (Step 7) | Optional (can be replaced) |

API keys go in `.env` (see `.env.example` if you add one — this repo doesn't ship any secrets).

---

## Methodology attribution

The system is opinionated and stands on the shoulders of several public methodologies. The `knowledge_base/` folder contains the canonical references:

- **Content Unit Framework** (Hook + Retain + Reward) — referenced in `knowledge_base/methodology/content-unit-framework.md`
- **Hormozi Content Structure Formula** (One Idea + Stories + Reasons + Soft CTA) — referenced in `knowledge_base/methodology/hormozi-content-structure-formula.md`
- **Audience as a compounding asset** — Hormozi, $100M Leads — `knowledge_base/business/audience-as-compounding-asset.md`
- **Creator benchmark** — 366-post analysis of 7 top GTM LinkedIn creators (April 2026) — `creator-benchmark.md`

---

## Contributing

This is an MVP extraction. Issues, pull requests, and forks are welcome. Particularly valuable:

- **New hook templates** (add to `skills/04-hook-generator.md`, show evidence of performance)
- **Better grading rubrics** (edit `skills/06-post-grader.md`, explain why)
- **Updated creator benchmark** (replace `creator-benchmark.md` with a fresh scrape)
- **Additional research workers** (add a file under `skills/` and register it in the orchestrator)
- **Adapters for non-LinkedIn platforms** (the repurpose skill is the natural seam)

Please keep PRs focused and include a short note on what signal you used to decide the change was worth it.

---

## License

MIT — see [`LICENSE`](LICENSE). Use it, fork it, productize it, ship it.

---

## Status

**MVP.** The pipeline works end-to-end in a production agency workflow. Expect rough edges when you wire up external APIs — not every integration is fully automated yet, and several steps are intentionally human-in-the-loop.

If you ship something interesting with this, open an issue — always curious what people build on top of it.
