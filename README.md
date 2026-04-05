<div align="center">

<pre>
 ██████╗ ██╗   ██╗  █████╗
██╔════╝ ██║   ██║ ██╔══██╗
██║      ╚██╗ ██╔╝ ███████║
██║       ╚████╔╝  ██╔══██║
╚██████╗   ╚██╔╝   ██║  ██║
 ╚═════╝    ╚═╝    ╚═╝  ╚═╝
</pre>

### CONTENT VISIBILITY AUDIT
**A Claude Code skill for content strategists and digital marketers.**

*See before you build.*

<br>

<img src="https://img.shields.io/badge/version-1.3-000000?style=flat-square" alt="version">&nbsp;<img src="https://img.shields.io/badge/free-open%20source-111111?style=flat-square" alt="free">&nbsp;<img src="https://img.shields.io/badge/Claude%20Code-skill-CC0000?style=flat-square" alt="Claude Code skill">

<br>

`/content-audit` &nbsp;·&nbsp; `/content-audit-setup`

</div>

---

## What this is

A Claude Code slash command skill that runs a full content visibility audit against your existing content program. It maps every asset to a funnel stage, flags what is gated and invisible to Google and AI, scores each page against EEAT and AEO frameworks, identifies where the funnel breaks, and delivers a prioritized action plan — all before recommending a single new piece of content.

It connects directly to GA4, Google Search Console, and Semrush to pull live data. It crawls pages with WebFetch for EEAT and AEO scoring. It runs keyword gap analysis against approved competitors with two guardrail gates before any cluster expansion. And it includes a standalone Content Map mode for mapping an entire resource library to funnel stages and identifying what to build or reposition.

This is not a content creation tool. It is a content diagnosis tool.

---

## Why it was built

Most content teams produce without a clear picture of what they already have, what is performing, what is invisible, and where the funnel breaks. The typical workflow is: write more, publish more, hope it works.

The Content Visibility Audit flips that. Before any new content gets produced, you need to see clearly:

- What exists and where it sits in the funnel
- What is gated and therefore invisible to Google and AI answer engines
- What is ranking but not converting, or visible but not ranking
- Where competitors are capturing keyword clusters you are not covering
- Which assets are failing EEAT or AEO quality thresholds
- What gaps can be filled by repositioning existing assets before writing anything new

Production is the last resort. This skill makes that principle actionable.

---

## Who this is for

- **Content strategists** who manage a content program and want to understand what is actually working before making production decisions
- **Digital marketers** focused on organic search and AI answer engine visibility
- **SEO practitioners** who want to integrate behavioral signal (GA4) and visibility signal (Search Console) with quality scoring (EEAT/AEO) in a single workflow
- **Solo operators and small teams** running a content program without a large agency or dedicated analytics function
- **Anyone who has been told to "create more content"** and wants to understand why the existing content is not converting first

---

## Version highlights

**v1.3** — Config path consistency fixes across Competitor Selection Gate and Layer 10; Keyword Gate 1 now runs in Content Map Mode before Gate 2, matching the full two-gate keyword workflow from Layer 5.

**v1.2** — Added Competitor Selection Gate (interactive, always-confirmed, three options); Layer 10 Content Map Mode (nine-step standalone strategic workflow); 3-mode return launch (Rerun / Single asset / Content map); version check on every launch with silent update notification.

**v1.1** — Output folder rule; context isolation rule; GA4 MCP connection option; WebFetch-based EEAT/AEO scoring; scale handling for large inventories; Layer 9 report saving; multi-domain config support.

**v1.0** — Initial release. Nine-layer audit framework, two-phase onboarding, EEAT + AEO scoring, competitor gap analysis, repurposing layer, MOFU-first prioritization.

Full history: [CHANGELOG.md](CHANGELOG.md)

---

## Install

### Mac / Linux

```bash
mkdir -p ~/.claude/commands && curl -fsSL https://raw.githubusercontent.com/drew-rewired/content-visibility-audit/main/content-audit.md -o ~/.claude/commands/content-audit.md
```

Restart Claude Code. Onboarding starts automatically on next launch.

---

### Windows

```powershell
curl.exe -fsSL https://raw.githubusercontent.com/drew-rewired/content-visibility-audit/main/content-audit.md -o "$env:USERPROFILE\.claude\commands\content-audit.md"
```

---

### Manual

[**Download content-audit.md →**](https://raw.githubusercontent.com/drew-rewired/content-visibility-audit/main/content-audit.md) *(right-click → Save As)*

Place the file in:
- **Mac / Linux**: `~/.claude/commands/`
- **Windows**: `%USERPROFILE%\.claude\commands\`

Restart Claude Code. Onboarding starts automatically.

---

## Getting started

**First launch:** Onboarding begins automatically — no slash command needed. You are walked through two phases:

1. **Technical connections** — GA4, Google Search Console, Semrush, competitor domains. All optional except your domain. If GA4 is connected via Claude MCP, just say "MCP" to skip manual configuration.
2. **Brand configuration** — Primary audience, ICP, brand voice, content goals, off-limits topics, and a free-text additional context field.

The only required answer is your domain. Everything else is optional — skipped steps are flagged and setup keeps moving.

Configuration saves to `content-audit/{domain}/content-audit-config.json` in your working directory.

**After setup:** Type `run audit` or `full audit` to begin. To update your configuration at any time, type `/content-audit-setup`.

---

## How it works

### On first run

Type `run audit` after setup completes. The skill pulls your full content inventory from Search Console (first), GA4 (fallback), or a manual URL list (last resort). Then it runs all nine audit layers in sequence.

### On return launches

You are presented with three modes:

| Mode | What it does |
|---|---|
| **Rerun audit** | Full re-audit with fresh data from all connected sources |
| **Single asset diagnostic** | Drop in one URL or PDF — runs all nine layers scoped to that asset |
| **Content map** | Maps your resource library to funnel stages, identifies gaps, produces keyword-backed recommendations |

Type `run audit` or `full audit` at any point to skip the menu and go straight to a full audit.

---

## The nine audit layers

| Layer | What it does |
|---|---|
| 1. Content inventory | Builds the asset list from Search Console → GA4 → manual upload, in that order |
| 2. Funnel mapping | Assigns every asset to TOFU, MOFU, or BOFU based on topic, framing, and searcher intent |
| 3. Gating audit | Fetches each page with WebFetch and flags every gated asset as a visibility failure |
| 4. Three-source triangulation | Combines GA4 behavioral signal, Search Console visibility signal, and Semrush intent classification |
| 5. Competitor gap analysis + keyword strategy | Competitor Selection Gate → gap analysis → two-gate keyword workflow with explicit approval before cluster expansion |
| 6. EEAT + AEO scrub | Fetches and scores every page for Google quality signals (EEAT) and AI answer extractability (AEO) — 100-point rubrics, YMYL-aware |
| 7. Gap identification | Maps what is missing in the sequence a buyer would actually follow |
| 8. Repurposing layer | Checks whether existing assets can fill gaps before recommending net-new production |
| 9. Output | Prioritized action plan: fix → reposition → ungate → produce. Saves as `content-audit-report.md` |

### Layer 10 — Content Map Mode

A standalone strategic workflow triggered from the return launch menu. Nine steps: asset intake, funnel placement, competitor + keyword context (with both keyword gates), performance signal, EEAT/AEO quick score, gap analysis, reposition check, recommendations, and content map output saved as `content-map.md`.

---

## Competitor Selection Gate

Before any competitor analysis runs — in the full audit or Content Map mode — you choose one of three options:

1. **Use saved competitors** — runs against the list from your config (shown for confirmation)
2. **Enter different competitors** — provide a new list; optionally save to config
3. **Discover via Semrush** — pulls domains with highest keyword overlap; shows the list for approval before running anything

No competitor analysis begins until you confirm the set.

---

## EEAT + AEO scoring

Every asset is scored on two independent 100-point rubrics.

**EEAT** (Expertise, Experience, Authoritativeness, Trustworthiness) — 25 points per dimension. YMYL content (health, finance, legal, safety) is held to stricter passing thresholds. Non-YMYL programs skip per-asset YMYL detection and apply standard thresholds across the board.

**AEO** (Answer Engine Optimization) — Six signals scored Full / Partial / None: declarative headers, paragraph density, self-contained sections, schema markup, answer-first structure, and inline term definitions.

Each asset receives a letter grade (A–F) on both frameworks and a priority flag: Immediate, Moderate, Monitor, or Pass.

---

## What you need

| Item | Required? | What it unlocks |
|---|---|---|
| Domain | Yes | Everything |
| GA4 Property ID (or MCP connection) | No | Behavioral signal — sessions, engagement, conversions |
| Google Search Console credentials | No | Visibility signal — impressions, CTR, position, top queries |
| Semrush API key | No | Keyword intent, competitor gap data, volume and difficulty |
| Competitor domains (up to 5) | No | Competitor gap analysis |

The skill runs without any of the optional items. Each missing source narrows the diagnostic — the audit will tell you exactly what is unavailable and what that means for each layer.

---

## Update notifications

The skill checks for updates on every launch. If a newer version is available, it surfaces a one-line notice with the update command. If it fails or you are current, nothing appears.

To update manually at any time:

```bash
curl -fsSL https://raw.githubusercontent.com/drew-rewired/content-visibility-audit/main/content-audit.md -o ~/.claude/commands/content-audit.md
```

Then restart Claude Code.

---

## Disclaimer

Outputs are AI-generated and provided as-is. They may contain errors or inaccuracies. Always verify data directly in your source systems (GA4, Semrush, Google Search Console) before making decisions. The creator assumes no responsibility for outcomes resulting from use of this tool's output.

---

## Bonus

A Content Repurpose Skill is available in the `bonus/` folder of this repo — for transforming existing assets into different formats and channels.

---

*Built by Drew Martinez · [drewmartinez.io](https://drewmartinez.io)*
