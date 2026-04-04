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

[![version](https://img.shields.io/badge/version-1.0-000000?style=flat-square)](https://github.com/drew-rewired/content-visibility-audit)&nbsp;[![free](https://img.shields.io/badge/free-open%20source-111111?style=flat-square)](https://github.com/drew-rewired/content-visibility-audit)&nbsp;[![Claude Code](https://img.shields.io/badge/Claude%20Code-skill-CC0000?style=flat-square)](https://github.com/drew-rewired/content-visibility-audit)

<br>

[![Install in Claude Code](https://img.shields.io/badge/%E2%96%B6%20%20INSTALL%20IN%20CLAUDE%20CODE-000000?style=for-the-badge)](claude://install-skill?url=https://raw.githubusercontent.com/drew-rewired/content-visibility-audit/main/content-audit-skill.md)

*Opens Claude Code and installs automatically.*

<br>

`/content-audit` &nbsp;·&nbsp; `/content-audit-setup`

</div>

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

The skill runs nine layers in sequence, regardless of whether you are auditing a single asset or a full content inventory.

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

## Install

### Option A — One click

Click the button at the top of this page. It opens Claude Code and installs the skill automatically.

---

### Option B — Manual install

**Step 1.** Download the skill file:

&nbsp;&nbsp;&nbsp;&nbsp;[**Download content-audit-skill.md →**](https://raw.githubusercontent.com/drew-rewired/content-visibility-audit/main/content-audit-skill.md) &nbsp;*(right-click → Save As)*

&nbsp;&nbsp;&nbsp;&nbsp;[**Download full repo as .zip →**](https://github.com/drew-rewired/content-visibility-audit/archive/refs/heads/main.zip)

**Step 2.** Place the file in your Claude Code skills folder. Copy the path for your OS:

Mac / Linux:
```
~/.claude/skills/
```

Windows:
```
%USERPROFILE%\.claude\skills\
```

Create the folder if it does not exist.

**Step 3.** Restart Claude Code. Onboarding starts automatically — no slash command needed on first launch.

---

## How it works

The first time Claude Code loads after install, onboarding starts automatically. It walks through two phases: technical connections (GA4, Search Console, Semrush, competitors) and brand configuration (audience, ICP, voice, goals, plus a free-text additional context field). The only required answer is your domain. Everything else is optional — if you skip a step, the skill flags what will be limited and keeps moving. Configuration saves to a local file called `content-audit-config.json`.

After that, type `/content-audit` to start an audit. The skill loads your config silently and asks how you want to begin: full content inventory, build from Search Console data, or single-asset diagnostic. Type `/content-audit-setup` at any time to update credentials, brand context, competitors, or anything else.

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
