# Setup Positioning Vault

> **⭐ Start here.** Run this before any other skill.

Bootstraps a complete PositioningHQ workspace for a company in a single guided session. After running, all other skills (`/battlecard`, `/call-plan`, `/product-launch`) will have the context they need from memory — no copy-pasting required.

## Command

```
/setup-positioning-vault
```

## What It Does

In one session, this skill:

1. **Asks for your vault root path** — any absolute or relative path (e.g. `/Users/you/vaults/acme` or `./acme-vault`). Defaults to `./positioning-vault` if none provided.
2. **Creates the vault folder structure** — `memory/`, `outputs/`, `knowledgebase/` and all subfolders
3. **Writes `vault.config.md`** — a status tracker at the vault root, updated automatically as each skill runs
4. **Collects company information** — name, website, industry, one-line product description, and 2–3 main competitors (all required)
5. **Runs `/company-research`** — full 9-step research, stored in `memory/company-research/[CompanyName].md`
6. **Runs `/positioning-playbook`** — 7-section playbook, stored in `memory/positioning-playbook/[CompanyName].md`
7. **Prints a vault-ready summary** — lists what was created and what skills to run next

## Vault Layout Created

```
VAULT_ROOT/
├── memory/
│   ├── company-research/       ← populated by this skill
│   └── positioning-playbook/   ← populated by this skill
├── inputs/                     ← drop reference materials here anytime
│   ├── sales collateral/
│   ├── competitive-intel/
│   ├── roadmap/
│   ├── help-docs/
│   ├── customer references/
│   └── company strategy/
├── outputs/
│   ├── battlecards/
│   ├── call-plans/
│   └── launch/
└── vault.config.md             ← status tracker
```

## vault.config.md

The tracker file is created at the vault root and updated by each skill as it completes:

```markdown
# PositioningHQ Vault

**Created:** 2026-03-12
**Vault Root:** /Users/you/vaults/acme

## Company
- **Name:** Acme Corp
- **Website:** acmecorp.com

## Status
- [x] Company Research
- [x] Positioning Playbook
- [ ] Battlecards
- [ ] Call Plans
```

## Notes

- If a vault already exists at the path (detected via `vault.config.md`), the skill asks whether to **reinitialise** or **update** — it will not silently overwrite memory files.
- All paths written to files use the absolute version of `VAULT_ROOT` for portability.
- Refer to [`references/vault-structure.md`](references/vault-structure.md) for the full canonical folder layout and naming conventions.

## What to Run Next

| Skill | Command | Uses vault? |
|---|---|---|
| Competitive Battlecards | `/battlecard` | ✅ Auto-loads playbook |
| Sales Call Prep | `/call-plan` | ✅ Auto-loads playbook |
| Product Launch | `/product-launch` | ✅ Auto-loads playbook |

---

← [Back to plugin README](../../README.md)
