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

![Version](https://img.shields.io/badge/version-1.0-000000?style=flat-square)&nbsp;
![Free](https://img.shields.io/badge/free-open%20source-111111?style=flat-square)&nbsp;
![Claude Code](https://img.shields.io/badge/Claude%20Code-skill-CC0000?style=flat-square)

<br>

### ▶ &nbsp;[INSTALL IN CLAUDE CODE](claude://install-skill?url=https://raw.githubusercontent.com/drew-rewired/content-visibility-audit/main/content-audit-skill.md)

*Click the link above to open Claude Code and install automatically.*

<br>

`/content-audit` &nbsp;·&nbsp; `/content-audit-setup`

</div>

---

## What this is

A Claude Code skill that audits your existing content program before making any production recommendations. It maps every asset to a funnel stage, flags gated content that is invisible to Google and AI search, identifies where the funnel is breaking down, and delivers a prioritized action plan. Built on one principle: production is the last resort.

---

## What you need

**Required:**
- A domain to audit

**Optional but recommended:**
- GA4 Property ID + Google Analytics Data API enabled
- Google Search Console API credentials (service account JSON from Google Cloud Console)
- Semrush API key
- Up to five competitor domains

The skill runs without the optional items. GA4 gives you behavioral signal. Search Console gives you visibility signal. Semrush gives you keyword intent and competitor gap data. Without them, the audit runs on structure alone — still useful, but less precise.

---

## Manual install

1. Download `content-audit-skill.md` from this repo.
2. Place it in your Claude Code skills folder:
   - **Mac / Linux**: `~/.claude/skills/`
   - **Windows**: `%USERPROFILE%\.claude\skills\`
   - Create the folder if it does not exist.
3. Restart Claude Code. Onboarding starts automatically.

---

## How it works

The first time you open Claude Code after installing, onboarding begins automatically — no slash command needed. You will be walked through setup in two phases: technical connections (GA4, Search Console, Semrush, competitors) and brand configuration (audience, ICP, voice, goals, plus an open-ended additional context field). The only required answer is your domain. Everything else is optional and flagged if skipped. Configuration saves to a local file called `content-audit-config.json`.

From that point forward, type `/content-audit` to start an audit. The skill loads your saved configuration silently and asks how you want to begin: full inventory, build from Search Console data, or single-asset diagnostic. Type `/content-audit-setup` at any time to update credentials, brand context, competitor domains, or anything else.

---

## Bonus

A Content Repurpose Skill is available in the `bonus/` folder of this repo.

---

*Built by Drew Martinez. [drewmartinez.io](https://drewmartinez.io)*
