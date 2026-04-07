<div align="center">

<img src="content_map_terminal-outlined.svg" alt="Content Map Skill">

### CONTENT MAP SKILL
**A Claude Code skill for content strategists and digital marketers.**

*See before you build.*

<br>

<img src="https://img.shields.io/badge/version-2.4-000000?style=flat-square" alt="version">&nbsp;<img src="https://img.shields.io/badge/free-open%20source-111111?style=flat-square" alt="free">&nbsp;<img src="https://img.shields.io/badge/Claude%20Code-skill-CC0000?style=flat-square" alt="Claude Code skill">

<br>

`/content-map` &nbsp;·&nbsp; `/content-map-setup`

</div>

---

**Mac / Linux**

```bash
mkdir -p ~/.claude/commands && curl -fsSL https://raw.githubusercontent.com/drew-rewired/content-map/main/content-map-skill.md -o ~/.claude/commands/content-map.md
```

**Windows**

```powershell
curl.exe -fsSL https://raw.githubusercontent.com/drew-rewired/content-map/main/content-map-skill.md -o "$env:USERPROFILE\.claude\commands\content-map.md"
```

Restart Claude Code. Onboarding starts automatically.

---

## What this is

A Claude Code slash command skill that maps your full content program before you make a single production decision. It maps every asset to a funnel stage, flags what is gated and invisible to Google and AI, scores each page against EEAT and AEO frameworks, identifies where the funnel breaks, and delivers a prioritized action plan — all before recommending a single new piece of content.

It connects directly to GA4, Google Search Console, and Semrush to pull live data. It crawls pages with WebFetch for EEAT and AEO scoring. It runs keyword gap analysis against approved competitors with two guardrail gates before any cluster expansion.

This is not a content creation tool. It is a content diagnosis tool.

---

## Skill flow

```
┌─────────────────────────────────────────────────────────────────────────┐
│  /content-map  ──  content audit + strategy                            │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Integrations ──  GA4 · Google Search Console · Semrush               │
│                   (all optional — map runs without them)               │
│                                                                         │
│    ┌───────────────┬──────────────────────┬────────────────────┐       │
│    │ Full inventory│  Google Search       │  Single diagnostic │       │
│    │               │  Console             │                    │       │
│    └───────┬───────┴──────────────────────┴────────────────────┘       │
│            │                                                            │
│  ── audit ──────────────────────────────────────────────────────────  │
│   Layer 1  ──  Inventory                                               │
│   Layer 2  ──  Funnel mapping              TOFU · MOFU · BOFU         │
│   Layer 3  ──  Gating audit                                            │
│   Layer 4  ──  Performance triangulation   ◄── GA4 · Search Console   │
│   Layer 5  ──  Competitor gap analysis     ◄── Semrush                │
│   Layer 6  ──  EEAT / AEO / GEO scrub                                 │
│  ── strategy ───────────────────────────────────────────────────────  │
│   Layer 7  ──  Gap identification + citation approval                  │
│   Layer 8  ──  Repurposing check  (reposition before net-new)         │
│   Layer 9  ──  Output → content-map-report.md                         │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
                   │
                   │  content-map-report.md loaded automatically
                   ▼
┌─────────────────────────────────────────────────────────────────────────┐
│  /content-remix  ──  content generation                                │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  Input ──  URL · PDF · doc · image · transcript · brief                │
│                                                                         │
│   Gate 1    ──  Input detection + funnel stage                         │
│   Gate 1.5  ──  Output stage lock  (same · reposition)                │
│   Gate 2    ──  Output format  (12 options)                            │
│   Gate 3    ──  Subtype                                                │
│   Gate 4    ──  Organic or paid                                        │
│   Gate 5    ──  Audience confirmation                                  │
│   Gate 6    ──  Research mode + citation approval                      │
│   Gate 7    ──  Job name + pre-run confirmation                        │
│                                                                         │
│   Generation + EEAT / AEO / GEO review + Quality Gate                │
│                                                                         │
│  Output ──  blog post · landing page · white paper · ebook            │
│             email sequence · social posts · podcast script            │
│             presentation · infographic brief · video script           │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

Pairs with the **[Content Remix Skill](https://github.com/drew-rewired/content-remix)** — once you know what to act on, remix takes those assets and rebuilds them for every channel and format you need.

---

## Who this is for

- **Content strategists** who manage a content program and want to understand what is actually working before making production decisions
- **Digital marketers** focused on organic search and AI answer engine visibility
- **SEO practitioners** who want to integrate behavioral signal (GA4) and visibility signal (Search Console) with quality scoring (EEAT/AEO) in a single workflow
- **Solo operators and small teams** running a content program without a large agency or dedicated analytics function
- **Anyone who has been told to "create more content"** and wants to understand why the existing content is not converting first

---

## How it works

**First launch:** Onboarding begins automatically — no slash command needed. You are walked through two phases:

1. **Technical connections** — GA4, Google Search Console, Semrush, competitor domains. All optional except your domain. If GA4 is connected via Claude MCP, just say "MCP" to skip manual configuration.
2. **Brand configuration** — Primary audience, ICP, brand voice, content goals, off-limits topics, and a free-text additional context field.

The only required answer is your domain. Everything else is optional — skipped steps are flagged and setup keeps moving.

Configuration saves to `content-map-config.json` in your current working directory.

**After setup:** Type `/content-map` to begin. To update your configuration at any time, type `/content-map-setup`.

### On return launches

You are presented with three modes:

| Mode | What it does |
|---|---|
| **Full inventory** | Full re-map with fresh data from all connected sources |
| **Single asset diagnostic** | Drop in one URL or PDF — runs all nine layers scoped to that asset |
| **Google Search Console** | Pulls indexed pages from the API and builds the inventory from that data |

---

## The nine map layers

| Layer | What it does |
|---|---|
| 1. Content inventory | Builds the asset list from Search Console → GA4 → manual upload, in that order |
| 2. Funnel mapping | Assigns every asset to TOFU, MOFU, or BOFU with a secondary user intent type (Know/Evaluate/Do) — flags intent mismatches |
| 3. Gating audit | Fetches each page with WebFetch and flags every gated asset as a visibility failure |
| 4. Performance triangulation | Combines GA4 behavioral signal, Search Console visibility signal, and Semrush intent classification |
| 5. Competitor gap analysis | Competitor Selection Gate → gap analysis → two-gate keyword workflow with explicit approval before cluster expansion |
| 6. EEAT, AEO, and GEO scrub | Fetches and scores every page across all three frameworks — YMYL flag for healthcare, finance, and legal domains |
| 7. Gap identification | Maps what is missing in the sequence a buyer would actually follow — with optional online research and per-citation approval |
| 8. Repurposing layer | Checks whether existing assets can fill gaps before recommending net-new production |
| 9. Output | Prioritized action plan: fix → reposition → ungate → produce. Saves as `content-map-report.md` |

---

## Competitor Selection Gate

Before any competitor analysis runs, you choose one of three options:

1. **Use saved competitors** — runs against the list from your config (shown for confirmation)
2. **Enter different competitors** — provide a new list; optionally save to config
3. **Discover via Semrush** — pulls domains with highest keyword overlap; shows the list for approval before running anything

No competitor analysis begins until you confirm the set.

---

## EEAT, AEO, and GEO scoring

Every asset is scored across three frameworks.

**EEAT** (Experience, Expertise, Authoritativeness, Trustworthiness) — Experience is flagged separately as the most commonly missing signal in B2B content. YMYL content (health, finance, legal, safety) triggers an elevated quality bar — missing or thin EEAT in YMYL domains is treated as a hard quality failure.

**AEO** (Answer Engine Optimization) — Six signals: declarative headers, paragraph density, self-contained sections, schema markup, answer-first structure, and inline term definitions. Chunk density check: sections should be 200–400 words; sections over 600 words without a structured break risk unpredictable AI chunking.

**GEO** (Generative Engine Optimization) — Signals for citation by AI-powered tools (ChatGPT, Perplexity, Google AI Overviews, Gemini): direct extractable answers, named entity references, verifiable factual claims, structured prose, citations present, and self-contained sections.

Each asset receives a letter grade (A–F) on all three frameworks. Layer 9 output includes an AEO + GEO readiness summary table: Asset | AEO Grade | GEO Grade | Top gap to fix.

---

## What you need

| Item | Required? | What it unlocks |
|---|---|---|
| Domain | Yes | Everything |
| GA4 Property ID (or MCP connection) | No | Behavioral signal — sessions, engagement, conversions |
| Google Search Console credentials | No | Visibility signal — impressions, CTR, position, top queries |
| Semrush API key | No | Keyword intent, competitor gap data, volume and difficulty |
| Competitor domains (up to 5) | No | Competitor gap analysis |

The skill runs without any of the optional items. Each missing source narrows the diagnostic — the map will tell you exactly what is unavailable and what that means for each layer.

---

## Update notifications

The skill checks for updates on every launch. If a newer version is available, it surfaces a one-line notice with the update command. If it fails or you are current, nothing appears.

To update manually at any time:

```bash
curl -fsSL https://raw.githubusercontent.com/drew-rewired/content-map/main/content-map-skill.md -o ~/.claude/commands/content-map.md
```

Then restart Claude Code.

---

Full changelog: [CHANGELOG.md](CHANGELOG.md)

---

## Disclaimer

Outputs are AI-generated and provided as-is. They may contain errors or inaccuracies. Always verify data directly in your source systems (GA4, Semrush, Google Search Console) before making decisions. The creator assumes no responsibility for outcomes resulting from use of this tool's output.

---

*Built by Drew Martinez · [drewmartinez.io](https://drewmartinez.io)*
