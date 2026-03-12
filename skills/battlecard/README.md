# Competitive Battlecards

Generates one markdown battlecard per competitor, designed for sales new hire enablement. Each battlecard is enriched with live web research on top of your vault's positioning playbook and knowledge base.

## Command

```
/battlecard
```

The skill will ask which competitors to generate cards for. You can specify one, several, or ask it to infer competitors from your playbook.

## What It Does

For each competitor:

1. **Loads context** from `memory/positioning-playbook/` and the `inputs/` subfolders (sales collateral, competitive intel, customer references, etc.)
2. **Runs web research** to enrich with current competitor positioning, recent news, and product updates
3. **Generates a structured battlecard** using the standard template

## Battlecard Contents

Each battlecard includes:

| Section | Contents |
|---|---|
| Competitor Overview | Who they are, positioning, ICP |
| Their Strengths | What they genuinely do well — no spin |
| Their Weaknesses | Product gaps, support issues, customer complaints |
| How We Win | Your key differentiators, head-to-head advantages |
| Landmine Questions | Discovery questions that expose competitor weaknesses |
| Objection Handling | "Why not [Competitor]?" responses with proof points |
| Proof Points | Quotes, case studies, win metrics relevant to this competitor |

## Output

One markdown file per competitor saved in your vault:

```
VAULT_ROOT/outputs/battlecards/battlecard-[competitor-name].md
```

**Example:** `battlecard-hubspot.md`, `battlecard-salesforce.md`

## Prerequisites

- Vault initialised via `/setup-positioning-vault` (or `memory/positioning-playbook/` populated manually)
- Web search enabled in Claude Code

## References

- [`assets/battlecard-template.md`](assets/battlecard-template.md) — standard battlecard structure
- [`references/battlecard-guidance.md`](references/battlecard-guidance.md) — section-by-section writing guidance

---

← [Back to plugin README](../../README.md)
