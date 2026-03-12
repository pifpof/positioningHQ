---
name: call-plan
description: Generates a personalized, stage-specific sales call plan as a Word doc (.docx). Use this skill whenever a rep asks to prepare for a sales call, create a call plan, prep for a discovery or demo meeting, or needs a pre-call brief for a specific prospect. Takes the positioning playbook plus prospect details as input — always researches the prospect company via web search before generating. Covers all sales cycle stages: discovery, demo, follow-up, and closing calls.
---

# Call Plan Skill

Generates a fully personalized call plan as a Word document (.docx), tailored to the prospect, the call stage, and the product's positioning. Follows the Command of the Message framework with best-practice sales structure.

---

## Step 1 — Collect Inputs

Ask the rep for the following. If any are missing, proceed with what's available and note gaps.

### Required
- **Positioning playbook** — internal doc with value props, ICP, differentiators, proof points
- **Prospect company name** — used for web research
- **Prospect's name and role/persona** — e.g. "Sarah, VP of RevOps"
- **Call stage** — ask the rep to choose:
  - `discovery` — first call, qualifying and diagnosing
  - `demo` — use-case focused product walkthrough
  - `follow-up` — progressing a deal, multi-stakeholder
  - `closing` — commercial negotiation, final objections

### Optional but valuable
- Known pain points or trigger events (e.g. funding, hiring push, new leadership)
- Tech stack / current tools in use
- Prior conversation notes or context from previous calls

---

## Step 2 — Research the Prospect Company

Always run web search on the prospect's company before generating the call plan. Search for:

1. `[company name] company overview` — size, industry, business model
2. `[company name] recent news` — funding, leadership changes, product launches, layoffs
3. `[company name] [prospect role]` — to understand likely priorities for that persona
4. `[company name] tech stack` or `[company name] uses [tool category]` — if tech stack wasn't provided

Use findings to:
- Personalise the opening hypothesis
- Identify trigger events that create urgency
- Tailor discovery questions to their likely situation
- Ground proof points in comparable companies or industries

---

## Step 3 — Select the Right Call Structure

Read `references/call-structures.md` to load the appropriate structure for the chosen call stage. Each stage has its own parts, timing, and objectives.

---

## Step 4 — Generate the Call Plan

Using the positioning playbook, prospect research, and the appropriate call structure from `references/call-structures.md`, generate a complete, personalised call plan.

Fill every section with specifics — no generic placeholders. If a section cannot be confidently personalised, mark it `⚠️ Research gap — confirm before call`.

Then output the call plan as a Word doc (.docx) using the docx skill.
Read `references/docx-output.md` for exact formatting and generation instructions.

---

## Step 5 — Deliver

Output:
- One `.docx` file named `call-plan-[prospect-company]-[stage]-[date].docx`
- A 2–3 sentence summary in the chat: prospect name, call stage, top hypothesis, and any research gaps flagged

---

## Quality Standards

- Write for the rep, not for the PMM — use direct, conversational language
- Every discovery question must be tied to a pain the positioning playbook identifies
- Proof points must come from the positioning playbook — never fabricate customer names or metrics
- The hypothesis must be specific to this prospect, not generic category pain
- Landmine questions must feel like natural discovery, not attacks
- The next step must be concrete — a specific ask, not "follow up"
