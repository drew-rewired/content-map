# Content Remix Skill

A Claude Code skill that takes any existing content asset and rebuilds it natively for every channel and format you need. Drop in a URL, PDF, white paper, transcript, or image — get back social posts, landing pages, email sequences, blog posts, podcast scripts, presentations, and more. Works best alongside the Content Map Skill but runs as a standalone tool without it.

---

## What you need

**Required:**
- A source asset in any format (URL, PDF, document, transcript, image)
- A domain

**Optional but recommended:**
- Content Map Skill installed and configured — adds keyword strategy, funnel context, and internal linking to every output
- Brand voice documentation — upload a brand guide or brief during onboarding to skip manual setup
- Semrush access — used in research mode to pull industry-specific data

---

## One-click install

[**Install Content Remix Skill →**](claude://install-skill?url=https://raw.githubusercontent.com/drew-rewired/content-map/main/bonus/content-remix-skill.md)

*Replace the URL above with the actual raw GitHub URL of `content-remix-skill.md` before publishing.*

---

## Manual install

1. [**Download content-remix-skill.md →**](https://raw.githubusercontent.com/drew-rewired/content-map/main/bonus/content-remix-skill.md) *(right-click → Save As)*
2. Place the file in your Claude Code commands folder:
   - **Mac / Linux**: `~/.claude/commands/`
   - **Windows**: `%USERPROFILE%\.claude\commands\`
3. Restart Claude Code. Onboarding starts automatically.

---

## How it works

The first launch runs a short onboarding — if you already have a brand guide or brief, you can upload it instead of answering setup questions manually. Works best when the Content Map Skill has been run on your domain first, but standalone is fine. Type `/content-remix` to start a new remix job. Type `/content-remix-setup` to update your configuration at any time. The skill learns your preferences and voice over time — format defaults, edit patterns, and approved outputs are stored locally and applied automatically on future runs.

---

## Main skill

The Content Map Skill is available at the root of this repo.

---

*Built by Drew Martinez. [drewmartinez.io](https://drewmartinez.io)*
