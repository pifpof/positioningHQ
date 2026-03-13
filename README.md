# PositioningHQ — Claude Code Plugin

[![Version](https://img.shields.io/badge/version-beta-blue.svg)](CHANGELOG.md)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/skills-6-purple.svg)](claude-plugin.json)

**A complete GTM and positioning intelligence suite for Claude Code.**  
Built for founders, PMMs, and sales leaders who want research, positioning, battlecards, call prep, and launch planning — all from a single plugin.

---

## Install

```bash
/install-plugin github.com/pifpof/positioningHQ
```

Once installed, all 6 slash commands are available in your Claude Code session.

---

## Skills

| Command | What it does | Output | Docs |
|---|---|---|---|
| `/setup-positioning-vault` | **⭐ Start here** — creates vault, collects company info, runs research + playbook | Vault folder + memory populated | [README](skills/setup-positioning-vault/README.md) |
| `/company-research <Company> \| <website>` | 9-step competitive & market research | `.md` in `memory/company-research/` | [README](skills/company-research/README.md) |
| `/positioning-playbook` | Full B2B positioning playbook (ICP → proof points) | `.md` in `memory/positioning-playbook/` | [README](skills/positioning-playbook/README.md) |
| `/battlecard` | One battlecard per competitor | Markdown per competitor in `outputs/battlecards/` | [README](skills/battlecard/README.md) |
| `/call-plan` | Personalised call plan for any deal stage | `.docx` in `outputs/call-plans/` | [README](skills/call-prep/README.md) |
| `/product-launch` | Full launch plan via founder interview | 6 files + impact assessment in `outputs/launch/` | [README](skills/product-launch/README.md) |

---

## Workflow

```
/setup-positioning-vault  →  (auto-runs /company-research + /positioning-playbook)
                                           ↓
                              /battlecard  ·  /call-plan  ·  /product-launch
```

1. **`/setup-positioning-vault`** — one-time setup: creates vault, collects company info, auto-runs research + playbook
2. **`/battlecard`** — equip your sales team with per-competitor battlecards
3. **`/call-plan`** — prep for any deal, any stage, any prospect
4. **`/product-launch`** — plan a launch end-to-end, including positioning impact assessment

---

## Prerequisites

- **Claude Code** (any tier)
- **Web search enabled** — several skills use web search to enrich research
- **Run `/setup-positioning-vault` first** — creates all required folders and populates memory automatically

---

## File Structure

```
positioninghq/
├── claude-plugin.json
├── README.md                   ← you are here
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
├── skills/
│   ├── setup-positioning-vault/
│   │   ├── README.md           ← skill docs
│   │   ├── SKILL.md
│   │   └── references/vault-structure.md
│   ├── company-research/
│   │   ├── README.md
│   │   ├── SKILL.md
│   │   └── assets/             # 9 step files (01–09)
│   ├── positioning-playbook/
│   │   ├── README.md
│   │   ├── SKILL.md
│   │   └── assets/             # 7 section files + sample template
│   ├── battlecard/
│   │   ├── README.md
│   │   ├── SKILL.md
│   │   └── assets/battlecard-template.md
│   ├── call-prep/
│   │   ├── README.md
│   │   ├── SKILL.md
│   │   └── references/
│   └── product-launch/
│       ├── README.md
│       ├── SKILL.md
│       └── references/
└── docs/                       # Marketplace website (GitHub Pages)
    ├── index.html
    └── skills/
```

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to submit improvements or new skills.

---

## License

MIT © [PositioningHQ](https://positioninghq.com)
