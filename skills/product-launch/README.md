# Product Launch

A 4-phase skill that generates a complete product launch plan through a structured founder interview. No documents required — just a conversation.

## Command

```
/product-launch
```

## Four Phases

### Phase 1 — Founder Interview
A conversational interview across 5 blocks: product, customer, market, launch context, and channels. 15–20 exchanges with follow-up probing on thin answers. The goal is to extract everything needed to write a launch that reflects your actual situation — not a generic template.

### Phase 2 — Strategy Checkpoint
Before generating anything, the skill summarises its understanding back to you for confirmation. This ensures the output reflects your intent.

### Phase 3 — Generate 6 Output Files
**Pass 1 (strategy layer)** — generated first. You review before Pass 2 begins.

| File | Contents |
|---|---|
| `launch-messaging-narrative.md` | Core message, value prop, audience definition, tone-of-voice |
| `launch-gtm-channel-plan.md` | Channel-by-channel plan grounded in your actual assets and budget |
| `launch-success-metrics.md` | 30-day and 90-day KPIs, leading indicators, tracking approach |

**Pass 2 (execution layer)** — generated after you approve Pass 1.

| File | Contents |
|---|---|
| `launch-sales-enablement-brief.md` | What sales needs: pitch, objections, competitive context |
| `launch-internal-faq.md` | Q&A for your team to speak confidently about the launch |
| `launch-announcement.md` | Ready-to-publish announcement for blog, email, or social |

### Phase 4 — Positioning Impact Assessment
Evaluates the launch across 5 dimensions and assigns a change rating (None / Partial / Full) for each:

| Dimension | Change Rating |
|---|---|
| Ideal Customer Profile (ICP) | None · Partial · Full |
| Market Segment | None · Partial · Full |
| Positioning & Category | None · Partial · Full |
| Value Drivers & Key Messages | None · Partial · Full |
| Differentiation & Brand Story | None · Partial · Full |

Based on the overall impact level (0–3), a `launch-positioning-update-recommendation.md` file is generated if warranted.

## Output

All files saved to:

```
VAULT_ROOT/outputs/launch/
```

## Optional Input

If a positioning playbook exists in `memory/positioning-playbook/`, the skill uses it as the baseline for the Phase 4 impact assessment.

## References

- [`references/interview-guide.md`](references/interview-guide.md) — structured interview question bank
- [`references/output-specs.md`](references/output-specs.md) — detailed specifications for all output files

---

← [Back to plugin README](../../README.md)
