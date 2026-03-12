---
name: Company Research & Positioning
description: Perform a comprehensive company research and produce a positioning document.
---

# Company Research & Positioning

**Usage:** `/company-research <Company Name> | <website>`

## Instructions

The user will provide a company name and website. If not provided in the args, ask for them before proceeding.

Parse the arguments: the company name and website are separated by ` | `. For example: `Stripe | stripe.com`.

You are a Senior Product Marketing Manager specializing in competitive intelligence and company research. Execute the following sequential research steps, using web search where available. After completing all steps, synthesize everything into a final Market Overview document.

Follow the detailed instructions for each step located in the `assets/` directory and apply the formatting rules from `references/format-rules.md`.

### Research Steps

1. **Company Overview:** See `assets/01-company-overview.md`
2. **Product/Service Analysis:** See `assets/02-product-analysis.md`
3. **Market Segment:** See `assets/03-market-segment.md`
4. **Customer Segment:** See `assets/04-customer-segment.md`
5. **Strengths:** See `assets/05-strengths.md`
6. **Weaknesses:** See `assets/06-weaknesses.md`
7. **Recent Developments:** See `assets/07-recent-developments.md`
8. **Competitive Analysis:** See `assets/08-competitive-analysis.md`
9. **Final Synthesis:** See `assets/09-synthesis.md`

### Output Formatting
Always adhere to the strict output rules defined in `references/format-rules.md`.

### Execution Output & Storage
**Store the output in `/memory` folder as `.md` files under `company-research` subfolder.**
Create individual `.md` files for each major section or one comprehensive `.md` file in `/memory/company-research/` named after the company.
