# Positioning Playbook

Generates a complete, 7-section, sales-ready positioning playbook. Designed to consume the output of `/company-research`, but works from any raw context you provide.

## Command

```
/positioning-playbook
```

## What It Does

Runs in three phases:

1. **Gather materials** — asks for supporting documents (pitch deck, case studies, customer testimonials, FAQs, existing sales decks). You can paste text or point to files. External research is also permitted.
2. **Sequential generation** — builds all 7 sections in order, each using its own asset file for guidance.
3. **Final deliverable** — saves the complete playbook to your vault.

## Playbook Sections

| # | Section | What it covers |
|---|---|---|
| 1 | Market Overview | "Why now?" narrative — tailwinds, shifts, market timing |
| 2 | Target Customers | ICP definition, persona breakdowns, jobs-to-be-done |
| 3 | Value Drivers | What customers actually buy and why — outcomes, not features |
| 4 | Distinct Advantages | Defensible differentiators — capabilities, moats, proof |
| 5 | Positioning Statement | The crisp "for X who Y, we are Z" statement and variations |
| 6 | Competitive Intelligence | Head-to-head comparison, win/loss patterns, competitive moves |
| 7 | Customer Proof Points | Quotes, metrics, case study summaries organized by persona |

## Output

A single structured markdown file stored at:

```
VAULT_ROOT/memory/positioning-playbook/[CompanyName].md
```

This file is automatically loaded by `/battlecard`, `/call-plan`, and `/product-launch`.

## When to Run

- **Run automatically** via `/setup-positioning-vault` — you usually don't need to run this directly
- **Run manually** to regenerate the playbook after new materials are available, or after significant product/market changes

## References

- [`assets/`](assets/) — 7 section-specific generation instruction files + sample playbook template
- [`references/tone-style.md`](references/tone-style.md) — tone and writing style guidelines

---

← [Back to plugin README](../../README.md)
