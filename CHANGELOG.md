# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.1.0] — 2026-03-12

### Added

- **`setup-positioning-vault` skill** — Onboarding skill that creates the vault folder structure (`memory/`, `outputs/`, `knowledgebase/`), collects company info, and auto-runs `/company-research` and `/positioning-playbook` in a single guided session. Includes a `vault.config.md` status tracker and reinitialisation detection.

### Changed

- Moved all skill folders into a `skills/` subdirectory for cleaner repo structure
- Updated all `claude-plugin.json` paths to use `skills/` prefix
- Bumped version to `1.1.0`

---

## [1.0.0] — 2026-03-12


### Added

- **`company-research` skill** — 9-step structured company research workflow producing a full market positioning document stored in `/memory/company-research/`
- **`positioning-playbook` skill** — 7-section B2B positioning playbook generator (ICP, value drivers, distinct advantages, positioning statement, competitive intelligence, customer proof points)
- **`competitive-battlecards` skill** — One-per-competitor markdown battlecards for sales new hire enablement, enriched with web search
- **`call-plan` skill** — Stage-specific (discovery / demo / follow-up / closing) personalized call plans output as `.docx`
- **`product-launch` skill** — Full launch plan via founder interview: 6 output files + Phase 4 positioning impact assessment
- `claude-plugin.json` plugin manifest
- `docs/` marketplace website (GitHub Pages)
- MIT License
