# Sales Call Prep

Generates a fully personalised, stage-specific sales call plan for any prospect. Always runs live web research on the prospect before generating. Output is a ready-to-use `.docx` file.

## Command

```
/call-plan
```

The skill will ask for:
- **Prospect company name and website**
- **Call stage** — discovery, demo, follow-up, or closing
- **Contact name and role** (if known)
- Any additional context (prior meeting notes, key pain points, deal status)

## What It Does

1. **Loads your playbook** from `memory/positioning-playbook/` for your product's positioning and messaging
2. **Researches the prospect** — company news, industry, role of the contact, recent activity
3. **Selects the right call structure** based on stage (guided by `references/call-structures.md`)
4. **Generates the call plan** — fully written, personalised to this specific prospect and deal
5. **Outputs a `.docx` file** using the formatting spec in `references/docx-output.md`

## Call Stages

| Stage | Call plan focuses on |
|---|---|
| Discovery | Hypothesis-driven questions, pain uncovering, qualification |
| Demo | Tailored demo flow, "show this, not that" guidance, proof points |
| Follow-up | Momentum maintenance, open items, next step commitment |
| Closing | Commercial terms framing, final objection handling, ask |

## Output

A `.docx` call plan file saved to:

```
VAULT_ROOT/outputs/call-plans/call-plan-[prospect]-[stage]-[YYYY-MM-DD].docx
```

**Example:** `call-plan-hubspot-discovery-2026-03-12.docx`

## Prerequisites

- Vault initialised via `/setup-positioning-vault` (or `memory/positioning-playbook/` populated manually)
- Web search enabled in Claude Code

## References

- [`references/call-structures.md`](references/call-structures.md) — call structure templates per stage
- [`references/docx-output.md`](references/docx-output.md) — `.docx` formatting and generation specification

---

← [Back to plugin README](../../README.md)
