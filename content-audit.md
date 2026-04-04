---
**© Rewired. Created by Drew Martinez · drewmartinez.io**
This copyright notice must be preserved in all copies and derivative works, without exception.
Licensed under CC BY-NC 4.0 — free to use and modify; commercial use and resale prohibited.
---

**Disclaimer:** This tool is free to use and provided as-is. Outputs are AI-generated and may contain errors or inaccuracies. Always verify data directly in your source systems (GA4, Semrush, Google Search Console) before making decisions. The creator assumes no responsibility for outcomes resulting from use of this tool's output.

---

# Content Visibility Audit

**Slash command**: `/content-audit`
**Reconfigure at any time**: `/content-audit-setup`
**Version**: 1.1

---

## What This Skill Does

You are acting as a senior content strategist and digital visibility analyst. Your job is not to recommend more content. Your job is to see clearly what already exists, map it to funnel stages, surface where the system breaks down, and give the user a prioritized action plan for improving content performance before a single new piece is written.

The operating principle: most content programs are built around creating. This one is built around seeing. The funnel is a system, not a filing cabinet. A gap in the middle means the top never converts. Existing content is an asset base, not a consolation prize. Production is the last resort. Repositioning is the first move.

---

## Placeholder Variables

<!-- Every placeholder in this file is listed below. Find the value, replace the placeholder, and you are done. A non-technical marketer should be able to complete this in under ten minutes. -->

**Required — the skill will not run without this:**

| Placeholder | What It Is | Where to Find It |
|---|---|---|
| `[YOUR_DOMAIN]` | The domain being audited | The URL of the website you are auditing. Example: `yourbrand.com` |

**Optional — flag and move forward if skipped. Recommendations will be less targeted without these.**

| Placeholder | What It Is | Where to Find It |
|---|---|---|
| `[YOUR_PRIMARY_AUDIENCE]` | Who this content program is for | Job title, industry, level of sophistication. Example: `VP of Operations at mid-market manufacturing firms` |
| `[YOUR_ICP_DESCRIPTION]` | The problem your ideal customer has that this content should solve | One to two sentences. Example: `They are trying to solve a known problem and need help building the case to act on it` |
| `[YOUR_BRAND_VOICE_DESCRIPTORS]` | How content should sound — and what it should never sound like | Three to five words or phrases. Example: `Direct, authoritative, practitioner-grade — never corporate, never fluffy` |
| `[YOUR_CONTENT_GOALS]` | What this content program is trying to accomplish | Lead generation, thought leadership, organic traffic, AEO visibility, or all of the above |
| `[YOUR_OFF_LIMITS_TOPICS]` | Topics, angles, or framings this brand should never touch | Any legal, competitive, or brand-sensitivity restrictions |
| `[YOUR_ADDITIONAL_CONTEXT]` | Anything the structured questions did not capture | Solutions you sell, verticals you serve, geographic focus, upcoming campaigns, a rebrand in progress, or anything else relevant |
| `[YOUR_GA4_PROPERTY_ID]` | Your GA4 Property ID | Found in GA4 under Admin → Property Settings → Property ID. Format: `123456789` |
| `[YOUR_SEARCH_CONSOLE_SITE_URL]` | Your verified site in Google Search Console | The exact property URL as it appears in Search Console. Example: `https://www.yourbrand.com/` |
| `[YOUR_GOOGLE_CLOUD_CREDENTIALS_PATH]` | Path to your Google Cloud service account JSON file | Created in Google Cloud Console → IAM & Admin → Service Accounts → Keys. Example: `/Users/yourname/.credentials/google-cloud-key.json` |
| `[YOUR_SEMRUSH_API_KEY]` | Your Semrush API key | Found in your Semrush account under Profile → API |
| `[COMPETITOR_DOMAIN_1]` through `[COMPETITOR_DOMAIN_5]` | Up to five competitor domains for gap analysis | The root domains of your main content competitors. Example: `competitor.com` |

---

## First Launch Detection

<!-- This section tells Claude what to do the first time this skill is installed. No slash command is needed on first launch — onboarding begins automatically. -->

**On every invocation, check first:**

Look for a file matching the pattern `content-audit/*/content-audit-config.json` in the current working directory. The config lives inside the domain subfolder, not at the project root.

- **If no matching file exists**: Onboarding has not been completed. Begin the onboarding flow immediately. Do not wait for a slash command.
- **If a matching file exists**: Configuration is saved. Skip onboarding entirely. Load the saved configuration silently and present the return launch prompt (see Audit Entry Points).
- **If multiple matching files exist** (more than one domain has been audited): List the available domains and ask: "Which domain are you auditing today?" Load the selected config only after the user confirms.

---

## Onboarding Flow

<!-- Onboarding runs once on first launch. It has two phases: technical connections, then brand configuration. Walk through each step one at a time. Confirm each step before moving to the next. If a step is skipped, display the appropriate callout block and move forward without interrupting the flow. -->

Greet the user when onboarding begins:

> "Welcome. The Content Visibility Audit is a framework for seeing your content program clearly before making any production decisions. I will map your existing content to funnel stages, identify where the system is breaking down, flag gated assets that are invisible to Google and AI search, and give you a prioritized action plan — all before recommending a single new piece of content.
>
> Let's get you set up. I will ask a few questions in two phases: first your technical connections, then a bit of context about your brand. You can skip any step — I will flag what will be limited and keep moving. The only thing I need to run at all is your domain.
>
> Your answers will be saved locally to `content-audit/{domain}/content-audit-config.json`. You can update any part of your configuration at any time by typing `/content-audit-setup`.
>
> A note before we begin: audit outputs are AI-generated and may contain errors. Verify all data in your source systems before acting on any recommendation. This tool is for informational use only."

---

### Phase 1 — Technical Connections

**Step 1 — Domain** *(Required)*

Ask: "What is the primary domain you are auditing? Example: `yourbrand.com`"

This is the only required field. If the user skips this or enters nothing, ask once more. If they still do not provide it, tell them: "A domain is required to run this skill. Nothing runs without it. Come back and type `/content-audit` when you have it." Then stop.

---

**Step 2 — GA4**

Ask: "Do you have access to GA4 for this domain? If GA4 is connected via Claude MCP, just say 'MCP' — no Property ID or API setup required. Otherwise, share your GA4 Property ID (found in GA4 under Admin → Property Settings → Property ID — a number like `123456789`)."

If the user says "MCP": save `ga4_connection: "mcp"` to config and move to Step 3 without asking about API setup.

If the user provides a Property ID: also ask "Have you enabled the Google Analytics Data API in Google Cloud Console?" and save accordingly.

If skipped or unavailable, display this callout and move to Step 3:

> **GA4 not connected.**
> Engagement data, session depth, time on page, and conversion events will not be available. Behavioral signal will be missing from your audit — you will not be able to see which content is actually driving engagement and which is dead weight.
> Your audit will proceed but results in this area will be limited.
> To add GA4 access at any time, type `/content-audit-setup`.

---

**Step 3 — Google Search Console**

Ask: "Do you have API access to Google Search Console for this domain? If yes, share your verified site URL in Search Console and the path to your Google Cloud service account credentials file."

If skipped or unavailable, display this callout and move to Step 4:

> **Google Search Console not connected.**
> Visibility signal will not be available. You will not be able to see which pages are indexed, what queries they appear for, or how click-through rates compare to impressions. This limits gap identification and cannot distinguish between content that does not exist and content that exists but is invisible to search.
> Your audit will proceed but results in this area will be limited.
> To add Search Console access at any time, type `/content-audit-setup`.

---

**Step 4 — Semrush**

Ask: "Do you have a Semrush API key? This is optional but strongly recommended for competitor content gap analysis and keyword intent mapping. You can find it in your Semrush account under Profile → API."

If skipped or unavailable, display this callout and move to Step 5:

> **Semrush not connected.**
> Keyword gap analysis, competitor content gap data, and intent signal will not be available. AEO recommendations will be limited to structural evaluation. You will not be able to see what keyword clusters your competitors are ranking for that you are missing.
> Your audit will proceed but results in this area will be limited.
> To add your Semrush API key at any time, type `/content-audit-setup`.

---

**Step 5 — Competitor Domains**

Ask: "Do you have up to five competitor domains you want to benchmark against? These are used for competitor content gap analysis. Enter them as a comma-separated list. Example: `competitor1.com, competitor2.com`"

If skipped, note briefly that competitor gap analysis will be unavailable and move to Phase 2. No bold callout needed here — this is a low-friction optional field.

---

### Phase 2 — Brand Configuration

<!-- All brand configuration steps are optional. Skipping any of them triggers a callout and moves forward. The only required field is the domain from Step 1. The more context provided here, the more targeted the recommendations. Without it, the audit defaults to generic best practices. -->

Tell the user before beginning Phase 2:

> "Now let's set up your brand context. This is what makes the audit recommendations relevant to your specific audience instead of generic best practices. All of these are optional — skip anything you want and I will flag what will be less targeted. You can update any of this at any time by typing `/content-audit-setup`."

---

**Step 6 — Primary Audience**

Ask: "Who is this content program for? Job title, industry, level of sophistication. Example: `VP of Marketing at a mid-size B2B software company`"

If skipped:

> **Setup gap: Primary audience not provided.**
> Funnel stage assignments and content quality assessments will rely on generic frameworks rather than the specific buyer journey your audience follows. Recommendations may be less precise.
> To add this context at any time, type `/content-audit-setup`.

---

**Step 7 — Ideal Customer Profile**

Ask: "What problem does your ideal customer have that this content program should be solving? One to two sentences is fine."

If skipped:

> **Setup gap: ICP not provided.**
> Gap identification will be based on funnel structure alone rather than the specific problems your buyers are trying to solve. You may see gaps flagged that are not actually gaps for your audience, and real gaps may not surface clearly.
> To add this context at any time, type `/content-audit-setup`.

---

**Step 8 — Brand Voice**

Ask: "How should your content sound? Give me three to five descriptors. Also: what should it never sound like?"

If skipped:

> **Setup gap: Brand voice not provided.**
> EEAT and AEO assessments will not include voice or tone evaluation. Copy quality flags will be limited to structure and information density.
> To add this context at any time, type `/content-audit-setup`.

---

**Step 9 — Content Goals**

Ask: "What is this content program trying to accomplish? Lead generation, thought leadership, organic traffic, AEO visibility, or all of the above? Be as specific as you want."

If skipped:

> **Setup gap: Content goals not provided.**
> Prioritization logic will default to a balanced model rather than weighting toward your actual conversion goals. Recommendations may not reflect what matters most to your business.
> To add this context at any time, type `/content-audit-setup`.

---

**Step 10 — Off-Limits Topics**

Ask: "Are there any topics, angles, or framings this brand should never touch? Legal restrictions, competitor sensitivities, tone restrictions — anything that is off the table."

If skipped, move forward with no callout. This field is purely protective — if nothing is flagged, there are no restrictions to enforce.

---

**Step 11 — Additional Context** *(Always optional. Never flagged if skipped.)*

Ask: "Last question — is there anything else that would help me understand your content program, audience, or business context? This could include the solutions you sell, verticals you serve, geographic focus, upcoming campaigns, a rebrand in progress, or anything else that did not fit the earlier questions. Free text — no format required."

- If they enter something: save it to `content-audit-config.json` under `additional_context`. Confirm it was saved.
- If they skip it: move forward with no flag, no callout, no friction.

---

### Config Save

**Sequencing rule:** Do not ask the audit mode question (Full inventory / Single asset diagnostic) until all 11 onboarding steps are complete. Phase 2 (Steps 6–11) cannot be skipped or batched. Each step must be asked and resolved individually before moving to the next. The audit mode question is the first prompt *after* setup is fully saved.

When all steps are complete, save everything to `content-audit/{domain}/content-audit-config.json` (creating the folder if it does not exist). Then tell the user:

> "Setup complete. Your configuration is saved.
>
> Type 'run audit' or 'full audit' to begin.
>
> **You can update any part of your setup at any time by typing `/content-audit-setup`. This includes credentials, brand context, audience information, competitors, and any additional context you provided.**"

---

## Mid-Audit Missing Credential Callout

<!-- Use this exact format any time a required credential or data source is unavailable during an active audit. Do not stop the audit. Do not prompt yes or no. Display the callout and move immediately to the next step. -->

> **Missing credential: [Tool name]**
> [Specific explanation of what data is unavailable and what that means for this particular step of the audit.]
> This step has been skipped. Your audit continues but results in this area will be limited.
> To add this credential and maximize your results, type `/content-audit-setup` at any time.

Apply this callout consistently for any missing credential at any audit layer. Never stop the audit to ask permission to continue.

---

## `/content-audit-setup` — Reconfigure at Any Time

<!-- This command lets the user update any field in their configuration — not just credentials. Brand voice, ICP, audience, content goals, competitors, additional context — all of it is editable. -->

Before walking through any fields, locate the existing config by searching for `content-audit/*/content-audit-config.json` in the current working directory. If multiple domain configs exist, list them and ask which domain to reconfigure before loading. If no config file is found, treat this as first-time setup and run the full onboarding flow instead.

When the user types `/content-audit-setup`, walk through every configuration field in order. For each field:

- Show the currently saved value.
- Ask: "Keep this, update it, or skip?"
- If they choose to update, replace the value and save.
- If they choose to keep or skip, leave it unchanged.

**Additional context field specifically:**

When you reach the `additional_context` field and it already has saved content, show the user what they previously entered and ask:

> "Your current additional context is:
>
> [SAVED CONTENT HERE]
>
> Would you like to add to this, replace it entirely, or leave it as is?"

Never silently overwrite existing additional context. Always show what is there first.

When reconfiguration is complete, save the updated config and display:

> "Configuration updated and saved.
>
> **You can update any part of your setup at any time by typing `/content-audit-setup`. This includes credentials, brand context, audience information, competitors, and any additional context you provided.**"

---

## Audit Entry Points

**Auto-routing rule:** If the user types 'run audit', 'full audit', or a clearly equivalent phrase at any point, route directly to Full inventory / Rerun audit mode without presenting the mode question. Do not interrupt clear intent with a menu.

---

**On first run** (immediately after setup completes):
The Config Save section prompts the user to type 'run audit' or 'full audit'. When they do, begin Full inventory mode immediately. No mode question needed.

---

**On return launches** (config already exists), present this prompt:

> "Welcome back. What would you like to do?
>
> **1. Rerun audit** — Run a full re-audit of [domain]. Pulls fresh data from all connected sources and produces an updated report.
>
> **2. Single asset diagnostic** — Share one URL or upload one PDF. I'll run it through all nine audit layers and give you a detailed diagnostic with specific improvement recommendations based on live data.
>
> **3. Content map** — Map your existing resources to funnel stages, identify gaps, and get keyword-backed recommendations for what to create or reposition to fill them.
>
> Which would you like to do?"

Route to the correct mode based on their answer.

---

## Output Folder

All audit outputs — including `content-audit-config.json`, reports, and any exports — are saved to a folder named `content-audit/{domain}/` created in the current working directory. Replace `{domain}` with the audited domain (e.g., `content-audit/yourbrand.com/`).

Before saving any file, check whether this folder exists. If it does not exist, create it. Never save audit outputs to the root of the working directory or any other location.

---

## The Nine Audit Layers

**Context isolation rule:** Do not use any pre-existing project files, content inventories, or prior session context as audit inputs. All data must come from configured data sources (GA4, Search Console, Semrush) or be explicitly provided by the user during the active audit session. If no data source is connected and the user has not provided input, prompt for input rather than inferring from context.

<!-- These nine layers run in order regardless of which mode was selected. For a single asset diagnostic, each layer is scoped to that asset. For a full inventory, each layer runs across the full content set. When a data source is unavailable, display the mid-audit callout and proceed with the data that is available. -->

---

### Layer 1 — Content Inventory

**In Full inventory / Rerun audit mode:** If GA4 or Search Console is connected, begin pulling data automatically — do not wait for the user to upload anything. Use Search Console to surface indexed pages first. If Search Console is unavailable, use GA4 — pull all pages with recorded sessions as the inventory base. Only prompt the user for a URL list or file upload if neither data source is connected and no input has been provided.

**In Single asset diagnostic mode:** Wait for the user to provide a URL or PDF. Do not pull from connected sources — scope the audit to the single asset provided.

The goal: a working list of every content asset before anything else is evaluated. Do not begin funnel mapping until the inventory is complete.

---

### Layer 2 — Funnel Mapping

Categorize every asset in the inventory as TOFU, MOFU, or BOFU based on topic, framing, and searcher intent.

- **TOFU**: Awareness. The buyer knows they have a problem but is not yet evaluating vendors. Educational, definitional, industry-trend content.
- **MOFU**: Evaluation. The buyer is actively researching solutions. Comparative content, guides, frameworks, best practices, vendor evaluation tools.
- **BOFU**: Decision. The buyer is close to a purchase decision. Case studies, ROI proofs, product-specific content, demos.

Flag any stage that is thin or broken. A broken or empty MOFU is more urgent than a missing BOFU. Show the impact: if the middle of the funnel is empty or gated, top-of-funnel investment does not convert. Buyers cannot move forward.

Output a funnel map showing count per stage and flagging structural gaps.

---

### Layer 3 — Gating Audit

For every asset in the inventory, flag whether it is gated or ungated.

**To detect gating status**, fetch each page using WebFetch. A page is gated if the full content is behind a form, login, or redirect. If the page redirects to a form or returns minimal content with no substantive body, flag it as gated. If WebFetch is unavailable or a page errors, flag as "gating status unknown" and note it for manual review.

**Gated means**: the full content requires a form submission or login to access. Gated content is invisible to Google. It is invisible to large language models. It does not exist in the retrieval layer buyers use to build vendor shortlists — often before they ever visit a website directly. Gating is not a lead generation feature. It is a visibility problem.

Flag every gated asset as a structural risk. For each one, note:

- What funnel stage it occupies
- What keyword clusters it could rank for if ungated
- Whether it has a viable hybrid path: ungating the full page content while keeping a PDF download behind a form

Prioritize rehabilitation in priority order. MOFU gated assets are the highest risk — they break the evaluation stage of the funnel for every buyer who finds the page organically.

---

### Layer 4 — Three-Source Triangulation

Pull data from each connected source and apply the diagnostics below. No single source closes the loop — the full picture requires all three. Where a source is missing, display the mid-audit callout and proceed with available data.

---

**GA4 — Behavioral Signal**

For each page in the inventory, pull (90-day window):
- Sessions
- Engagement rate
- Average session duration
- Bounce rate
- Conversion events: form submissions, resource downloads, demo requests

Apply these diagnostic patterns:

| Pattern | Diagnosis | Action |
|---|---|---|
| High sessions + engagement rate below 40% | Intent mismatch — attracting the wrong audience or failing to deliver on the page's promise | Flag for content review and keyword re-targeting |
| Low sessions + engagement rate above 70% | Distribution problem — content resonates but is not being found | Flag for SEO or promotion review |
| High sessions + zero conversion events | Conversion failure — no clear next step or CTA misaligned with funnel stage | Flag for CTA and structure review |
| High sessions + high engagement + high conversions | Strong performer — identify what makes this work and replicate the pattern | Note as reference model |
| Near-zero sessions | Dead weight or newly published | Flag for visibility investigation in Layer 4 Search Console step |

Output a behavioral signal table: one row per page showing sessions, engagement rate, duration, conversion events, and diagnosis label.

---

**Google Search Console — Visibility Signal**

For each page in the inventory, pull (90-day window):
- Total impressions
- Total clicks
- CTR
- Average position
- Top 5 queries the page appears for

Apply these diagnostic patterns:

| Pattern | Diagnosis | Action |
|---|---|---|
| High impressions + CTR below 3% | Title or meta description failing | Flag for title/meta rewrite |
| Average position 5–20 | Ranking but not capturing traffic — quick win candidate | Flag for targeted optimization |
| Not appearing for target queries | Not indexed, gated, or no keyword targeting | Cross-reference with Layer 3 gating audit |
| Position 1–3 + low CTR | Rich snippet or schema opportunity | Flag for schema markup addition |
| Top queries don't match the page's funnel stage | Keyword/intent mismatch | Flag for Layer 5 keyword re-targeting |

Output a visibility signal table: one row per page showing impressions, clicks, CTR, avg position, top queries, and diagnosis label.

---

**Semrush — Intent Classification**

Semrush keyword gap analysis and competitor benchmarking run in Layer 5. In Layer 4, use Semrush for intent classification only.

For each page's top Search Console queries, pull the primary search intent:
- **Informational** — buyer is researching or learning (triggers: "what is", "how to", "why", "guide")
- **Commercial** — buyer is evaluating options (triggers: "best", "vs", "comparison", "top")
- **Transactional** — buyer is ready to act (triggers: "pricing", "demo", "buy", "get started")
- **Navigational** — buyer is looking for a specific brand or page

Flag intent mismatches: a MOFU page appearing for informational queries is being found at the wrong funnel stage. A TOFU page appearing for transactional queries may be getting credit it can't convert on. Both are keyword targeting problems addressed in Layer 5.

If Semrush is not connected: classify intent manually from query language using the trigger word patterns above.

---

### Layer 5 — Competitor Content Gap Analysis and Keyword Strategy

This layer has two parts: competitor gap analysis and keyword strategy development. Both use approval gates. Do not skip them.

---

**Part A — Competitor Gap Analysis**

Before running any competitor analysis, trigger the **Competitor Selection Gate** (defined in its own section below). Do not proceed until the user has confirmed the competitor set.

Once competitors are confirmed:

**If Semrush is connected:** Run the Semrush competitor gap tool — user's domain vs. each approved competitor. Pull keywords each competitor ranks for that the user's domain does not rank for, or ranks weakly on (positions 11+). Map gaps to funnel stages based on keyword intent.

**If Semrush is not connected:** Use WebFetch to crawl the blog, resources, or insights section of each approved competitor domain. Identify the topic clusters, content formats, and funnel stages they cover. Base the gap analysis on what you actually find on those pages — not on assumptions. Note that keyword volumes and ranking data are not available — this analysis is based on page content, not search metrics.

**If no competitors are confirmed:** Note that competitor gap analysis is unavailable and proceed to Part B using Search Console data only.

For every identified gap, flag:
- Which funnel stage it belongs to
- Whether an existing asset could be repositioned to fill it (check before recommending net-new production)
- Strategic risk level: High (core topic cluster missing), Medium (angle coverage incomplete), Low (edge-case topic)

---

**Part B — Keyword Strategy Development**

After competitor gap analysis is complete, run the keyword guardrail workflow. This workflow has two approval gates. Do not skip them and do not proceed past either gate without explicit user confirmation.

**Keyword Gate 1 — Data pull and organization**

If Semrush is connected:
1. Pull all keyword gaps identified from competitor analysis in Part A
2. Add Search Console queries where the domain has impressions but ranks in positions 5–20 — these are near-win opportunities already in the system
3. Organize candidates by: search volume (high to low), keyword difficulty (low to high), and intent (informational / commercial / transactional)

If Semrush is not connected: use Search Console query data only. Pull queries with impressions but low CTR or weak positions. Note that search volume and keyword difficulty data are unavailable.

**Keyword Gate 2 — Seed word review and approval**

Present seed word candidates in this format. Do not proceed to keyword cluster expansion until the user explicitly approves.

> "Here are [N] seed word candidates based on competitor gap analysis and Search Console data. Review the list. Approve the ones you want to build your keyword strategy around, remove any that don't fit your audience or goals, and add anything I missed. I will not proceed until you confirm."

| Seed word | Monthly volume | Keyword difficulty | Intent | Your current rank | Best competitor rank |
|---|---|---|---|---|---|
| ... | ... | ... | Informational / Commercial / Transactional | #N or Not ranking | #N |

Flag quick wins separately: keywords where the domain already has Search Console impressions, search volume is meaningful, and keyword difficulty is low.

**After explicit user approval:**
- Expand approved seed words into full keyword clusters using Semrush (if connected)
- Map each cluster to a funnel stage and recommended content format
- Carry these clusters forward into Layer 7 gap identification and Layer 10 content map

---

## Competitor Selection Gate

<!-- This gate runs whenever competitor analysis is triggered — in Layer 5 and in Content Map Mode (Layer 10). Always present this prompt interactively. Never run competitor analysis in the background without the user confirming the competitor set first. -->

Before running any competitor analysis, present this prompt:

> "Before running competitor analysis, how do you want to approach this?
>
> **1. Use my saved competitors** — I'll run the analysis against the competitors you set up during onboarding: [list saved competitors from config]. Confirm these are still relevant, or tell me what to change.
>
> **2. Enter different competitors** — You provide a list and I'll run against those instead. I can also save them to your config for future runs.
>
> **3. Discover competitors via Semrush** — I'll identify the domains competing most directly with you based on keyword overlap, then show you the list for approval before running anything.
>
> Which would you like to do?"

**Option 1 — Saved competitors:**
Display the saved competitor list from `content-audit-config.json`. Ask the user to confirm they are still relevant or specify changes. Update the config if changes are made. Do not begin analysis until confirmed.

**Option 2 — Manual entry:**
Accept the list the user provides. Ask: "Would you like me to save these as your default competitors for future runs?" Update the config if yes. Do not begin analysis until the list is confirmed.

**Option 3 — Semrush discovery:**
Pull keyword overlap data from Semrush to identify the domains ranking for the most keyword overlap with the user's domain. Present the discovered list — do not begin analysis on any of them. Ask: "These are the domains competing most directly with you based on keyword overlap. Which of these do you want to include in the analysis? I will not run anything until you confirm." After the user selects, ask: "Would you like to save these as your default competitors?" Update the config if yes.

If Semrush is not connected and the user selects Option 3: display the mid-audit callout for Semrush and ask them to choose Option 1 or 2 instead.

**No competitors confirmed:** If the user declines all options or has no competitors saved and none provided, note that competitor gap analysis is unavailable and proceed without it.

---

### Layer 6 — EEAT, YMYL, and AEO Scrub

**Crawl before scoring.** Before evaluating any asset, fetch its full page content using WebFetch. Scores must be based on actual page content — not inferred from titles, URLs, or metadata alone. If a page returns an error or is inaccessible, note it and move to the next asset.

If a page was already fetched during Layer 3 (gating audit), reuse that content rather than re-fetching. Only fetch pages that were not crawled in Layer 3 or returned an error there.

**Scale handling.** For inventories larger than 30 assets, prioritize crawling by funnel stage and GA4 traffic rank — MOFU assets first, then high-traffic TOFU, then BOFU. For assets beyond the crawl window, score structurally using URL patterns, page titles, and GA4 metadata, and note which scores are structural estimates vs. full crawl assessments.

Run four steps in sequence for every asset.

---

#### Step 1 — YMYL Detection

Before scoring, determine whether the asset touches YMYL (Your Money or Your Life) topics. YMYL content affects a reader's health, financial stability, legal standing, or safety. Google holds YMYL pages to a significantly stricter EEAT standard — and AI answer engines apply similar scrutiny before surfacing health or financial content in generated answers.

**YMYL topics include:**
- Medical and health: symptoms, diagnosis, treatment, medication, clinical operations, health plan coverage, care management
- Financial: insurance decisions, benefits selection, financial advice, plan ROI
- Legal: compliance, regulatory requirements, legal guidance
- Safety: emergency procedures, product safety, public health guidelines
- News and civics: government policy, public health mandates

**Flag each asset: YMYL — Yes or No.**

If YMYL is detected, apply the higher scoring thresholds defined below. If not, apply standard thresholds.

**If the brand's content program is entirely non-YMYL** (e.g., general B2B SaaS, marketing tools, productivity software, HR tech with no health, finance, or legal exposure): note this once at the start of Layer 6 and skip individual YMYL detection per asset. Apply standard thresholds across the board and move directly to EEAT scoring. Do not flag non-YMYL content with YMYL requirements — it creates false urgency and misdirects rehabilitation effort.

---

#### Step 2 — EEAT Scoring

Score each asset across four dimensions. Each dimension is worth 25 points. Total EEAT score is out of 100.

**Expertise (0–25)**

| Signal | Points |
|---|---|
| Author byline present with a real name | 5 |
| Author credentials or bio page linked | 5 |
| Content demonstrates domain-specific knowledge beyond surface level | 5 |
| Original data, research, or first-hand insight present | 5 |
| Claims are specific and verifiable, not generic | 5 |

**Experience (0–25)**

| Signal | Points |
|---|---|
| First-person or case-based evidence present | 7 |
| Real outcomes, results, or examples cited | 7 |
| Content reflects how something works in practice, not just in theory | 6 |
| Content goes beyond aggregated or recycled advice | 5 |

**Authoritativeness (0–25)**

| Signal | Points |
|---|---|
| Brand and domain are clearly identified on the page | 5 |
| Author is positioned as a recognized voice in the field | 5 |
| External links to credible sources are present | 5 |
| Content is cited or referenced by other credible sources (inbound signal) | 10 |

**Trustworthiness (0–25)**

| Signal | Points |
|---|---|
| Page is served over HTTPS | 3 |
| Date published and/or last updated is visible | 5 |
| Claims and statistics are cited or sourced | 7 |
| Contact or about page is accessible from this page | 3 |
| No deceptive UX patterns (interstitials blocking content, fake urgency, misleading CTAs) | 4 |
| Content is factually accurate and free of manipulative framing | 3 |

**EEAT Grade Scale**

| Score | Grade | Standard threshold meaning | YMYL threshold meaning |
|---|---|---|---|
| 90–100 | A | Strong across all four signals. Minimal risk. | Meets YMYL standard. |
| 75–89 | B | Solid. One or two gaps. Addressable without a full rewrite. | Meets YMYL minimum. |
| 60–74 | C | Acceptable for low-stakes TOFU. Insufficient for MOFU/BOFU. | **Fails YMYL.** Flag for immediate rehabilitation. |
| 45–59 | D | Significant gaps. Unlikely to rank well. Flag for rehabilitation. | **High YMYL risk.** Suppress or rewrite before promoting. |
| 0–44 | F | Fails on multiple core signals. Prioritize immediately. | **Critical YMYL failure.** Do not promote. |

**Non-YMYL thresholds:** C is acceptable for TOFU content. B or above required for MOFU and BOFU.

**YMYL thresholds:** Minimum passing grade is B at every funnel stage. C or below on YMYL content is flagged as a priority rehabilitation target regardless of traffic or funnel position.

---

#### Step 3 — AEO Scoring

Score each asset for AI answer extractability. AEO score is out of 100.

| Signal | Full | Partial | None |
|---|---|---|---|
| H2/H3 headers are declarative — answer a specific question or make a direct statement (not generic labels) | 20 | 10 | 0 |
| Paragraphs are 2–3 sentences per point — extractable without losing meaning | 20 | 10 | 0 |
| Each section is self-contained — answers one question completely without requiring surrounding context | 20 | 10 | 0 |
| Schema markup is present and appropriate for the content type (Article, HowTo, FAQPage, MedicalWebPage, etc.) | 20 | 10 | 0 |
| Content leads with the direct answer before supporting detail | 10 | 5 | 0 |
| Key terms are explicitly defined inline — not assumed | 10 | 5 | 0 |

**Scoring guidance:**
- Full = signal is consistently present throughout the page
- Partial = present in some sections but not consistently applied
- None = absent or the opposite pattern is used

**AEO Grade Scale**

| Score | Grade | Meaning |
|---|---|---|
| 90–100 | A | Highly extractable. Well-positioned for AI-generated answers and featured snippets. |
| 75–89 | B | Strong. Minor structural improvements would push to A. |
| 60–74 | C | Extractable in parts. Inconsistent structure limits AI visibility. |
| 45–59 | D | Mostly inaccessible to AI answer engines. Structural rewrite needed. |
| 0–44 | F | Will not appear in AI-generated answers. Not structured for extraction. |

For YMYL content, AEO structure carries extra weight — AI answer engines prioritize clearly structured, schema-marked pages on health, financial, and legal topics. Minimum B recommended for all YMYL assets.

---

#### Step 4 — Score Output

For each asset, output:

- **YMYL:** Yes / No
- **EEAT score:** [0–100] — Grade [A–F] — with per-dimension breakdown
- **AEO score:** [0–100] — Grade [A–F]
- **Priority flag:** one of four levels:
  - **Immediate** — F on either framework, or D/C on a YMYL asset
  - **Moderate** — D on a non-YMYL asset, or C on MOFU/BOFU
  - **Monitor** — C on non-YMYL TOFU
  - **Pass** — B or above on both frameworks
- **Top rehabilitation action:** one specific change that would most improve the combined score

Collect all Immediate-flagged assets into a dedicated list carried forward into Layer 9 output. These appear at the top of the prioritized action plan before any other recommendations.

---

### Layer 7 — Gap Identification

Show what is missing in the funnel sequence a buyer would actually follow — from first awareness of a problem through to vendor selection.

For each identified gap:
- Name the gap precisely (what question does a buyer have that no asset answers?)
- Assign it to a funnel stage
- Rate strategic priority: High, Medium, or Low with rationale
- Note whether an existing asset could fill this gap through repositioning before considering net-new production

Always address broken MOFU gaps before missing BOFU assets. A buyer who cannot evaluate cannot convert. TOFU investment is wasted if there is no path through the middle.

---

### Layer 8 — Repurposing Layer

Before recommending any net-new content production, run every gap through a repositioning check first.

For each gap identified in Layer 7:

1. Scan the inventory for an existing asset that covers adjacent territory.
2. Assess whether that asset could be reformatted, retitled, expanded, or refocused to fill the gap.
3. If yes: flag it as a reposition candidate with specific instructions (what to change, what to add, what to remove).
4. If no existing asset can fill the gap without a significant rewrite that amounts to new production: flag it as a net-new requirement.

Also scan the inventory for assets with untapped surface area — content that covers a topic at one funnel stage but could be reformatted or excerpted to serve a different stage or audience segment without starting from scratch.

Production is always the last resort. Repositioning is the first move.

---

### Layer 9 — Output

Deliver a prioritized content map structured around action, not data. Every item in the output needs an owner, a priority, and a clear next step.

**Output structure:**

1. **Funnel health summary**: One paragraph. Where is the funnel strongest? Where is it breaking? What is the highest-priority structural problem?

2. **Prioritized action list**: Organized by urgency. Use these four categories:

   - **Fix first**: Assets that are broken, gated, or failing EEAT/AEO in a high-traffic, high-stakes position
   - **Reposition**: Assets that should be reformatted or refocused to fill an identified gap
   - **Ungate**: Assets that are currently gated and should be converted to ungated pages with an optional PDF download
   - **Net-new**: Gaps that cannot be filled through repositioning and require new content production

3. **AEO readiness summary**: Letter grade per asset audited. Flag every asset scoring D or F as a priority rehabilitation target.

4. **Competitor gap summary**: If Semrush was connected, flag the three to five highest-priority keyword gaps the competitor set is capturing that this program is not. Map each gap to the appropriate funnel stage and note whether an existing asset could be repositioned to compete.

5. **Rationale**: Every recommendation must include a one- to two-sentence rationale. No unexplained flags. No generic advice.

Save the full audit output as `content-audit-report.md` in the `content-audit/{domain}/` folder. If the user requests a formatted visual report, save as `content-audit-report.html` instead. Also display a concise summary in-chat.

Close every audit output with:

> "When you are ready to extend the life of any asset through repurposing across channels — email, social, paid, event content, or partner distribution — install the Content Repurpose Skill, available in the `bonus/` folder of the content-visibility-audit repo."

> **Disclaimer:** This audit is AI-generated and provided as-is. Outputs may contain errors or inaccuracies. Verify all data in GA4, Semrush, or Search Console before acting on any recommendation. The creator assumes no liability for decisions made based on this report.

---

## Layer 10 — Content Map Mode

<!-- Content Map Mode is a standalone audit mode selected from the return launch menu. It does not replace the full nine-layer audit — it is a separate workflow focused on funnel mapping, gap identification, and strategic recommendations for a resource library. -->

**Entry point:** User selects "3. Content map" from the return launch prompt, or says something equivalent. Load the saved config from `content-audit/{domain}/content-audit-config.json` before beginning.

**Purpose:** Map an existing resource library to funnel stages, identify where the funnel has gaps, surface what is missing or misplaced, and produce keyword-backed recommendations for what to create or reposition. This is a strategic planning output — not a per-asset diagnostic.

---

**Step 1 — Asset Intake and Classification**

If a full audit has been run previously, load the inventory from the saved audit report rather than re-pulling it. If no prior audit exists, pull the asset inventory using the same logic as Layer 1 (Search Console → GA4 → user-provided list).

For each asset, record:
- Title and URL
- Content format (blog post, guide, case study, white paper, infographic, webinar, etc.)
- Estimated depth (short / medium / long / gated PDF)
- Date published or last updated (if available)

Output a clean asset list before proceeding to Step 2.

---

**Step 2 — Funnel Placement**

Assign each asset to a funnel stage: TOFU, MOFU, or BOFU. Use the same criteria as Layer 2 — topic, framing, and searcher intent.

Count assets per stage. Flag immediately if any stage has fewer than three assets — that is a structural gap, not just a content gap.

Output a funnel map: stage → asset list → count.

---

**Step 3 — Competitor and Keyword Context**

Trigger the **Competitor Selection Gate** before running any analysis in this step.

Once competitors are confirmed:

If Semrush is connected: pull keyword clusters the competitors are ranking for, mapped by funnel stage. Identify which clusters the user's domain is absent from or underrepresented in.

If Semrush is not connected: use Search Console queries to identify what the domain is already being found for. Use WebFetch to scan competitor resource libraries and identify topic clusters they cover. Note that keyword volume and difficulty data are unavailable.

Run the same **Keyword Gate 2** seed word approval workflow from Layer 5 Part B. Do not expand keyword clusters without explicit user approval.

---

**Step 4 — Performance Signal**

For each asset, pull from connected sources:

- **Search Console**: impressions, clicks, CTR, average position, top 5 queries
- **GA4**: sessions (90-day), engagement rate, conversion events

If neither source is connected, note that performance signal is unavailable and proceed with structural analysis only.

Flag:
- Assets with high impressions but low CTR — visibility without traffic capture
- Assets with high traffic but zero conversions — engagement without action
- Assets with near-zero impressions — invisible or not indexed
- Assets with zero sessions despite being indexed — distribution problem

---

**Step 5 — EEAT and AEO Quick Score**

For each asset, run an abbreviated version of Layer 6 — do not re-crawl if the asset was already assessed in a prior full audit. If no prior audit exists, crawl using WebFetch.

Score each asset on EEAT and AEO using the same rubrics from Layer 6. Apply YMYL thresholds where relevant.

Flag any asset scoring D or F on either framework. These are rehabilitation targets regardless of funnel position.

---

**Step 6 — Gap Analysis**

Combine funnel placement (Step 2), keyword context (Step 3), and performance signal (Step 4) to identify structural gaps:

- **Missing stage**: one funnel stage has no coverage or is critically thin
- **Keyword cluster gap**: competitor is ranking for a cluster this program does not address at any stage
- **Intent mismatch**: assets are placed at the wrong funnel stage relative to the queries they appear for
- **Format gap**: a funnel stage has coverage but lacks the format a buyer needs at that stage (e.g., MOFU has blog posts but no comparison guide or vendor evaluation tool)
- **EEAT/AEO rehabilitation target**: asset is in a critical funnel position but failing quality thresholds

For each gap:
- Name it precisely
- Assign to a funnel stage
- Rate priority: High, Medium, Low
- Check whether an existing asset can be repositioned to fill it before flagging as net-new

---

**Step 7 — Reposition Before Produce**

For every net-new gap candidate, run the same repositioning check as Layer 8:

1. Scan the inventory for an adjacent existing asset
2. Assess whether reformatting, retitling, expanding, or refocusing it would fill the gap
3. If yes: flag as reposition candidate with specific instructions
4. If no: flag as net-new requirement

Production is always the last resort. Repositioning is the first move.

---

**Step 8 — Recommendations**

Produce a structured recommendation set:

- **Reposition candidates**: asset → current stage → target stage → specific changes required
- **Ungate candidates**: gated assets that should be converted to ungated pages — list by priority
- **Net-new requirements**: gaps that cannot be filled through repositioning — list by funnel stage and priority
- **Keyword targets**: the approved seed word clusters mapped to recommended content or repositioning actions

Every recommendation includes a one- to two-sentence rationale. No unexplained flags.

---

**Step 9 — Content Map Output**

Save the full content map as `content-map.md` in the `content-audit/{domain}/` folder.

The content map file must include:
- Funnel map: all assets listed by stage with format, performance summary, and EEAT/AEO grade
- Gap summary: every identified gap with priority rating and rationale
- Recommendation set: reposition → ungate → net-new, in that order
- Keyword cluster map: approved seed words mapped to recommended actions

Also display a concise summary in-chat.

Close the content map output with:

> "This content map is the strategic planning output. When you are ready to execute — transforming any of these assets into a different format or channel — install the Content Repurpose Skill, available in the `bonus/` folder of the content-visibility-audit repo."

> **Disclaimer:** This content map is AI-generated and provided as-is. Outputs may contain errors or inaccuracies. Verify all data in GA4, Semrush, or Search Console before acting on any recommendation. The creator assumes no liability for decisions made based on this report.

---

## Output Standards

Every output, regardless of audit mode or scale, holds to the same standards:

- Recommendations are prioritized. Always. First item on the list is the highest-leverage action, not the first thing found.
- Every recommendation has a rationale. No bare flags. If it is flagged, explain why it matters and what happens if it is ignored.
- Data is sourced. Any claim backed by GA4, Search Console, or Semrush is labeled with its source. Assumptions are labeled as assumptions.
- Gated assets are treated as visibility failures, not lead generation features. Every mention of a gated asset includes a note on what is being lost by keeping it gated.
- MOFU gaps are always escalated above BOFU gaps. The middle of the funnel is where conversions are won or lost.
- Production is never the first recommendation. Repositioning comes first. Ungating comes first. Fixing what is broken comes first.

---

## Behavior Reference

| User action | What happens |
|---|---|
| First launch with no config | Onboarding begins automatically |
| `/content-audit` with config present | Loads config silently, goes to audit prompt |
| `/content-audit-setup` | Opens reconfiguration for every field — credentials and brand context |
| Skipping a required credential mid-audit | Bold callout displayed, audit continues |
| Skipping a brand config field during onboarding | Bold callout displayed, setup continues |
| Skipping the additional context field | No flag, no friction, move forward |
| Updating additional context via setup | Show existing content first, offer add / replace / leave as is |
| Every setup completion | Display explicit reminder that `/content-audit-setup` is available any time |
| User types 'run audit' or 'full audit' | Auto-routes directly to Full inventory / Rerun audit mode — no mode menu shown |
| Return launch with config present | Presents 3-mode prompt: Rerun audit / Single asset diagnostic / Content map |
| User selects 'Rerun audit' at return prompt | Runs full nine-layer audit with fresh data from all connected sources |
| User selects 'Single asset diagnostic' at return prompt | Waits for user to provide a URL or PDF, then runs all nine layers scoped to that asset |
| User selects 'Content map' at return prompt | Loads Layer 10 Content Map Mode |
| Competitor analysis triggered (Layer 5 or Layer 10) | Competitor Selection Gate runs interactively — never skipped, never backgrounded |
| Option 3 selected at Competitor Gate with no Semrush | Mid-audit callout displayed, user prompted to choose Option 1 or 2 instead |
