<div align="center">

<pre>
 ██████╗ ██╗   ██╗  █████╗
██╔════╝ ██║   ██║ ██╔══██╗
██║      ╚██╗ ██╔╝ ███████║
██║       ╚████╔╝  ██╔══██║
╚██████╗   ╚██╔╝   ██║  ██║
 ╚═════╝    ╚═╝    ╚═╝  ╚═╝
</pre>

### CONTENT VISIBILITY AUDIT SKILL
**A Claude Code skill for content strategists and digital marketers.**

*See before you build.*

<br>

<img src="https://img.shields.io/badge/version-1.0-000000?style=flat-square" alt="version">&nbsp;<img src="https://img.shields.io/badge/free-open%20source-111111?style=flat-square" alt="free">&nbsp;<img src="https://img.shields.io/badge/Claude%20Code-skill-CC0000?style=flat-square" alt="Claude Code skill">

<br>

`/content-audit` &nbsp;·&nbsp; `/content-audit-setup`

</div>

---

## Install

### Mac / Linux — one command, copy and paste into your terminal

```bash
mkdir -p ~/.claude/skills && curl -fsSL https://raw.githubusercontent.com/drew-rewired/content-visibility-audit/main/content-audit-skill.md -o ~/.claude/skills/content-audit-skill.md
```

Restart Claude Code after running. Onboarding starts automatically.

---

### Windows — one command, paste into PowerShell

```powershell
curl.exe -fsSL https://raw.githubusercontent.com/drew-rewired/content-visibility-audit/main/content-audit-skill.md -o "$env:USERPROFILE\.claude\skills\content-audit-skill.md"
```

---

### Manual download

[**Download content-audit-skill.md →**](https://raw.githubusercontent.com/drew-rewired/content-visibility-audit/main/content-audit-skill.md) &nbsp;*(right-click → Save As)*

[**Download full repo as .zip →**](https://github.com/drew-rewired/content-visibility-audit/archive/refs/heads/main.zip)

Place the `.md` file in:
- **Mac / Linux**: `~/.claude/skills/`
- **Windows**: `%USERPROFILE%\.claude\skills\`

Then restart Claude Code. Onboarding starts automatically.

---

## Why this exists

Most content programs are built around creating. This one is built around seeing. Before any production recommendation is made, the full strategic state of the existing content program has to be visible.

The funnel is a system, not a filing cabinet. A gap in the middle means the top never converts. Gated content is invisible to Google and invisible to AI — it does not exist in the research layer buyers use to build vendor shortlists before ever visiting your website. And most content teams keep producing into a broken structure without knowing it.

This skill forces the audit before the output. It maps what you have, shows where it breaks, flags what is invisible, and delivers a prioritized action plan. Production is the last resort.

---

## Who this is for

- Content strategists managing a content program and trying to make it actually perform
- Digital marketers who want organic and AI visibility, not just more published pieces
- Solo operators running a content program without a large team or agency
- Anyone who has been told to "do more content" and wants to figure out why the existing content is not converting first

---

## What it audits

Nine layers run in sequence, regardless of whether you are auditing a single asset or a full content inventory.

| Layer | What it does |
|---|---|
| 1. Content inventory | Builds a working list of every asset from what you provide or Search Console data |
| 2. Funnel mapping | Assigns every asset to TOFU, MOFU, or BOFU based on topic and intent |
| 3. Gating audit | Flags every gated asset as a visibility problem, not a lead gen feature |
| 4. Three-source triangulation | Combines GA4 (behavior), Search Console (visibility), and Semrush (intent) |
| 5. Competitor gap analysis | Identifies what competitors rank for that your program is not covering |
| 6. EEAT + AEO scrub | Scores each asset for Google quality signals and AI answer extractability |
| 7. Gap identification | Shows what is missing in the sequence a buyer would actually follow |
| 8. Repurposing layer | Checks whether existing assets can fill gaps before recommending new production |
| 9. Output | Prioritized action plan: fix, reposition, ungate, or produce — in that order |

---

## How it works

After install, onboarding starts automatically on the next Claude Code launch — no slash command needed the first time. You will be walked through two setup phases: technical connections (GA4, Search Console, Semrush, competitors) and brand configuration (audience, ICP, voice, goals, plus a free-text additional context field). The only required answer is your domain. Everything else is optional — skipped steps are flagged and the setup keeps moving. Configuration saves locally to `content-audit-config.json`.

After that, type `/content-audit` to start an audit. Type `/content-audit-setup` at any time to update credentials, brand context, or anything else.

---

## What you need

**Required:**
- A domain to audit

**Optional but recommended:**
- GA4 Property ID + Google Analytics Data API enabled
- Google Search Console API credentials (service account JSON via Google Cloud Console)
- Semrush API key
- Up to five competitor domains

The skill runs without the optional items. GA4 gives you behavioral signal. Search Console gives you visibility signal. Semrush gives you keyword intent and competitor gap data. Without them, the audit runs on structure alone — still useful, but less precise.

---

## Bonus

A Content Repurpose Skill is available in the `bonus/` folder of this repo.

---

*Built by Drew Martinez. [drewmartinez.io](https://drewmartinez.io)*
