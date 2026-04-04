# Changelog

All notable changes to the Content Visibility Audit skill are documented here.

---

## [1.2] — 2026-04-04

### Added
- **Competitor Selection Gate** — Standalone interactive section (between Layer 5 and Layer 6) that runs whenever competitor analysis is triggered. Three options: use saved competitors, enter a manual list, or discover competitors via Semrush keyword overlap. Always requires explicit user confirmation before any analysis begins. Never runs in the background.
- **Layer 10 — Content Map Mode** — Standalone nine-step workflow for mapping a resource library to funnel stages, identifying gaps, and producing keyword-backed recommendations. Triggered from the return launch menu (option 3). Steps: asset intake and classification, funnel placement, competitor and keyword context (with gate), performance signal, EEAT/AEO quick score, gap analysis, reposition before produce, recommendations, content map output. Output saved as `content-map.md` in the domain folder.
- **3-mode return launch** — When a config already exists, the skill now presents three options: Rerun audit, Single asset diagnostic, or Content map. Previously, the return launch went directly to an audit prompt without offering mode selection.
- **Behavior Reference table updates** — Added rows for: auto-routing on "run audit" / "full audit", 3-mode return prompt, each return mode routing, Competitor Selection Gate trigger, and Semrush-unavailable fallback at the gate.

### Changed
- **Layer 5 reference** — Part A now explicitly references the Competitor Selection Gate as a defined section, not inline logic.
- **Version** — Bumped from 1.1 to 1.2.

---

## [1.1] — 2026-04-04

### Added
- **Disclaimer** — Added to file header, onboarding greeting, and every audit output. Outputs are AI-generated; users must verify data in source systems before acting.
- **GA4 MCP option** — Users with GA4 connected via Claude MCP can say "MCP" during Step 2 to skip Property ID and API setup entirely. Saves `ga4_connection: "mcp"` to config.
- **Phase 2 sequencing guardrail** — Audit mode question is explicitly blocked until all 11 onboarding steps are complete. Steps 6–11 cannot be skipped or batched.
- **Output folder rule** — All audit outputs (config, reports, exports) now save to `content-audit/{domain}/` in the current working directory. Folder is created automatically if it does not exist.
- **Context isolation rule** — Explicit instruction added to The Nine Audit Layers: audit inputs must come from configured data sources (GA4, Search Console, Semrush) or explicit user input only. Pre-existing project files and prior session context are excluded.
- **Layer 6 — WebFetch crawl** — EEAT/AEO scores must now be based on actual fetched page content via WebFetch. Scores inferred from titles, URLs, or metadata alone are not permitted.
- **Layer 6 — Scale handling** — For inventories over 30 assets, crawl priority is MOFU first → high-traffic TOFU → BOFU. Assets beyond the crawl window receive structural estimates, clearly labeled as such.
- **Layer 9 — Report saving** — Audit output now saves as `content-audit-report.md` in the domain folder by default. HTML version available on request. Concise in-chat summary always displayed regardless of format.
- **Multi-domain config handling** — When multiple domain configs exist (pattern `content-audit/*/content-audit-config.json`), the skill lists available domains and asks which to load before proceeding.

### Changed
- **Config file location** — Config now saves to `content-audit/{domain}/content-audit-config.json` (inside a domain subfolder), not the project root.
- **Config lookup** — First Launch Detection now searches the `content-audit/*/content-audit-config.json` pattern instead of a fixed root-level filename.
- **Layer 1 fallback order** — When Search Console is unavailable, GA4 page data (all pages with recorded sessions) is used as the inventory base. Manual URL list is only requested if both sources are unavailable.
- **Audit modes simplified** — Removed "Build from Search Console" as a standalone mode. Full inventory now handles auto-build from connected sources (GA4 and/or Search Console) automatically. Mode count reduced from 3 to 2.
- **Setup completion message** — Removed "Restart Claude Code and type /content-audit." Replaced with: "Your configuration is saved. Type 'run audit' or 'full audit' to begin."
- **Sequencing rule** — Mode list in Config Save guardrail updated from three modes to two: Full inventory / Single asset diagnostic.
- **Version** — Bumped from 1.0 to 1.1.

---

## [1.0] — Initial release

- Nine-layer content audit framework
- Two-phase onboarding: technical connections (GA4, Search Console, Semrush, competitor domains) + brand configuration (audience, ICP, voice, goals, off-limits topics, additional context)
- Three audit modes: Full inventory, Build from Search Console, Single asset diagnostic
- `/content-audit` and `/content-audit-setup` slash commands
- EEAT + AEO scoring with letter grades (A–F)
- Competitor content gap analysis via Semrush
- Repurposing layer evaluated before any net-new production recommendation
- MOFU gaps escalated above BOFU gaps throughout all output
