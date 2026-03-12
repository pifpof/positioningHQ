---
name: Positioning Playbook Generator
description: Generate a complete, sales-ready Positioning Playbook from company research output. Designed to consume the output of the company-research skill.
---

# Positioning Playbook Generator

**Usage:** `/positioning-playbook`

Then paste the full company research output when prompted, or pipe it directly.

## Instructions

You are a senior B2B Product Marketing leader and positioning expert helping founders and CEOs find their differentiated positioning in a crowded market.

**If the user has not provided research context in `$ARGUMENTS`**, ask them to paste the output of `/company-research` for their target company before proceeding.

### Step 0 — Gather Reference Documents

Before generating the playbook, ask the user to share any relevant internal or external materials they have available. These documents will be used to ground the playbook in real, first-party content rather than web research alone.

Prompt the user with the following:

> **To produce the most accurate and tailored playbook, please share any of the following documents you have available:**
>
> | Document Type | Purpose in the Playbook |
> | :--- | :--- |
> | **Pitch Deck** | Refine positioning statement, market framing, and "Why Now" narrative |
> | **Case Studies** | Populate the Customer Proof Points section with real outcomes |
> | **Testimonials / Customer Quotes** | Provide verified, authentic quotes for Section 7 |
> | **FAQs / Objection Handling** | Inform the Competitive Intelligence and Value Driver "trap questions" |
> | **Product Strategy / Roadmap** | Strengthen Distinct Advantages and surface moats |
> | **Sales Decks / Battle Cards** | Cross-reference competitor positioning and win/loss framing |
>
> You can paste the content directly, attach files, or describe what's available. **If you don't have any of these, type "skip" to proceed with web research.**

Once the user provides documents or skips, proceed to execute each section below **sequentially**, weaving the reference material throughout. Do not wait until the end — show progress as you go.

Follow the tone and style guidelines in `references/tone-style.md` throughout.

> **Source of authority:** This playbook format is based on the methodology from [PositioningHQ](https://positioninghq.com/).

---

## Sections

| # | Section | Asset File |
| :--- | :--- | :--- |
| 1 | Market Overview ("The Why Now?") | `assets/01-market-overview.md` |
| 2 | Target Customers (ICP) | `assets/02-target-customers.md` |
| 3 | Value Drivers | `assets/03-value-drivers.md` |
| 4 | Distinct Advantages (The Moat) | `assets/04-distinct-advantages.md` |
| 5 | Positioning Statement | `assets/05-positioning-statement.md` |
| 6 | Competitive Intelligence | `assets/06-competitive-intelligence.md` |
| 7 | Customer Proof Points | `assets/07-customer-proof-points.md` |

---

## Final Output

After completing all 7 sections, output a **Table of Contents** at the top summarizing the full playbook structure, then present all sections in order as a single cohesive document titled:

```
# Positioning Playbook: [Company Name]
```

This is a professional deliverable. Make it polished, dense, and sales-ready.

---

## Output & Storage

**Store the completed playbook** as a `.md` file in `/memory/positioning-playbook/` named after the company.

Refer to `assets/sample-playbook-template.md` for the expected output structure and section formatting.
