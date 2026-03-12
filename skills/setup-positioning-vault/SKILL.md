---
name: setup-positioning-vault
description: Initialises the PositioningHQ vault for a company. Creates the required folder structure, collects company details, and runs the company-research and positioning-playbook skills to populate the vault with foundational positioning context. Run this first whenever setting up a new company workspace. Accepts a custom root folder path.
---

# Setup Positioning Vault

Bootstraps a complete PositioningHQ workspace for a company in a single guided session. After running this skill, all other skills (`/battlecard`, `/call-plan`, `/product-launch`) will have the context they need from memory — no copy-pasting required.

---

## Step 1 — Choose Vault Root

Ask the user:

> **Where should the vault be created?**
>
> Provide an absolute or relative path to the folder that should serve as the vault root.
> For example: `/Users/yourname/vaults/acme` or `./acme-vault`
>
> The vault will be created there if it doesn't exist. All memory, outputs, and knowledge base files will be stored inside it.

Store the response as `VAULT_ROOT`. All subsequent folder creation and file paths in this skill use `VAULT_ROOT` as the base.

If the user does not provide a path, default to `./positioning-vault` and confirm:
> *"No path provided — I'll create the vault at `./positioning-vault`. Is that OK?"*

---

## Step 2 — Create Vault Folder Structure

Create the following folders inside `VAULT_ROOT`. If they already exist, skip without error.

Read `references/vault-structure.md` for the full canonical folder layout and the purpose of each folder.

```
VAULT_ROOT/
├── memory/
│   ├── company-research/       ← output of /company-research
│   └── positioning-playbook/   ← output of /positioning-playbook
├── inputs/                     ← drop your reference materials here
│   ├── sales collateral/
│   ├── competitive-intel/
│   ├── roadmap/
│   ├── help-docs/
│   ├── customer references/
│   └── company strategy/
├── outputs/
│   ├── battlecards/            ← output of /battlecard
│   ├── call-plans/             ← output of /call-plan
│   └── launch/                 ← output of /product-launch
└── vault.config.md             ← vault metadata file (created in Step 3)
```

After creating folders, confirm to the user:
> *"✅ Vault created at `VAULT_ROOT`. Here's what was set up: [list folders created]"*

---

## Step 3 — Write Vault Config

Create `VAULT_ROOT/vault.config.md` with the following content, filling in what's known at this stage:

```markdown
# PositioningHQ Vault

**Created:** [today's date]
**Vault Root:** [VAULT_ROOT]

## Company
- **Name:** (populated in Step 4)
- **Website:** (populated in Step 4)
- **Industry:** (populated in Step 4)

## Status
- [ ] Company Research
- [ ] Positioning Playbook
- [ ] Battlecards
- [ ] Call Plans
```

This file will be updated as each skill completes.

---

## Step 4 — Collect Company Information

Ask the user for the following. All are required before proceeding:

> **Let's set up your company profile.**
>
> 1. **Company name** — e.g. "Acme Corp"
> 2. **Company website** — e.g. "acmecorp.com"
> 3. **Industry / market category** — e.g. "B2B SaaS, revenue intelligence"
> 4. **Your product's one-line description** — e.g. "AI-powered sales forecasting for RevOps teams"
> 5. **Your 2–3 main competitors** — e.g. "Clari, Gong, Salesforce Forecasting"
>
> You can answer all five in one message.

Once collected, update `vault.config.md` with the company details.

---

## Step 5 — Run Company Research

Inform the user:
> *"Great — running `/company-research` for [Company Name] now. This will take a few minutes as I research and synthesise their market position."*

Execute the `company-research` skill using the company name and website collected in Step 4.

- Store output in `VAULT_ROOT/memory/company-research/[CompanyName].md`
- Update `vault.config.md`: mark `- [x] Company Research`

After completion, summarise what was found in 2–3 sentences and ask:
> *"Company research complete. Here's a quick summary: [summary]. Ready to generate the Positioning Playbook — want to drop any files into `inputs/` first (sales collateral, competitive intel, roadmap docs, etc.), or should I proceed with what I have?"*

---

## Step 6 — Run Positioning Playbook

Execute the `positioning-playbook` skill using:
- The company research output from Step 5
- Any additional materials provided by the user in response to the prompt above

- Store output in `VAULT_ROOT/memory/positioning-playbook/[CompanyName].md`
- Update `vault.config.md`: mark `- [x] Positioning Playbook`

---

## Step 7 — Vault Setup Complete

Print a final summary:

> **✅ PositioningHQ vault ready for [Company Name]**
>
> **Vault location:** `VAULT_ROOT`
>
> **What's been set up:**
> - ✅ Folder structure created
> - ✅ Company research complete → `memory/company-research/[CompanyName].md`
> - ✅ Positioning playbook complete → `memory/positioning-playbook/[CompanyName].md`
>
> **What you can run next:**
> - `/battlecard` — generate competitive battlecards using your playbook
> - `/call-plan` — prep for any sales call against a specific prospect
> - `/product-launch` — plan a product launch
>
> All skills will automatically load context from this vault.

---

## Quality Standards

- Never proceed past Step 4 without all 5 company details — they are required for research quality
- Do not skip the strategy checkpoint in Step 5: always summarise research before generating the playbook
- If the vault root already exists and contains a `vault.config.md`, read it first and ask: *"A vault already exists at this path for [Company]. Do you want to reinitialise it (this will overwrite memory files) or update it with new research?"*
- All paths written to files should use the absolute version of `VAULT_ROOT` so files can be found regardless of working directory
