# Company Research

Performs structured, 9-step competitive and market research on any company and saves the output to your vault.

## Command

```
/company-research <Company Name> | <website>
```

**Example:**
```
/company-research Stripe | stripe.com
```

## What It Does

Runs 9 sequential research steps, each guided by a dedicated asset file:

| Step | Focus |
|---|---|
| 1 | Company overview — founding story, business model, funding, team size |
| 2 | Product & platform analysis — features, pricing, architecture |
| 3 | Market segment — category, TAM, tailwinds, "why now" |
| 4 | Customer segment — ICPs, personas, jobs-to-be-done |
| 5 | Strengths — competitive moats, brand, execution |
| 6 | Weaknesses — gaps, limitations, customer complaints |
| 7 | Recent developments — fundraises, product launches, partnerships, exec changes |
| 8 | Competitive analysis — landscape map, head-to-head positioning |
| 9 | Final synthesis — positioning summary and strategic narrative |

## Output

A single structured markdown file stored at:

```
VAULT_ROOT/memory/company-research/[CompanyName].md
```

This file is automatically loaded by `/positioning-playbook` and `/battlecard`.

## When to Run

- **Run automatically** via `/setup-positioning-vault` — you usually don't need to run this directly
- **Run manually** when you want to refresh research on a company, or research a second company in the same vault

## References

- [`assets/`](assets/) — 9 step-by-step research instruction files (one per step)
- [`references/format-rules.md`](references/format-rules.md) — output formatting rules and conventions

---

← [Back to plugin README](../../README.md)
