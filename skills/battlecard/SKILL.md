---
name: competitive-battlecards
description: Generates competitive battlecards for sales new hire enablement. Use this skill whenever someone wants to create, update, or research competitive battlecards, compare against a competitor, build sales enablement material, prepare reps for competitive deals, or needs to know how to position against a specific rival. Accepts positioning playbook output, website/product docs, raw notes, and existing sales decks as input — and enriches with web search where gaps exist.
---

# Competitive Battlecards Skill

Generates one markdown battlecard per competitor, designed for sales new hire enablement. Each battlecard gives a rep everything they need to win a competitive deal.

## Inputs (use whatever is available)

Claude should ask the user to provide any of the following before starting:

1. **Positioning playbook** — internal doc describing your product's positioning, ICP, and value props
   - **First:** Check `/memory/positioning-playbook/` for an existing playbook for the target company.
   - **If found:** Load it automatically and confirm with the user: *"I found a positioning playbook for [Company] in memory — I'll use that as the foundation. Should I proceed?"*
   - **If not found:** Notify the user and offer to generate one: *"No positioning playbook found in memory for [Company]. I recommend running the `positioning-playbook` skill first to create one, which will make the battlecards significantly stronger. Should I do that now, or would you like to provide your own materials?"* If the user agrees, run the positioning-playbook skill and store the output in `/memory/positioning-playbook/` before continuing.
2. **Website / product docs** — your own product site or competitor's public site
3. **Raw notes** — anything the PMM or sales leader has written down
4. **Existing sales decks & knowledge base** — pitch decks, competitive slides, prior battlecards, FAQs, objection handling docs, case studies
   - **First:** Automatically read all files in `/memory/knowledgebase/` and extract any relevant content (competitive intel, positioning, objections, case studies, product details).
   - **Then:** Ask the user: *"I've read the following files from your knowledge base: [list files found]. Is there anything else you'd like to add — such as a recent pitch deck, objection handling doc, or case study — that isn't captured here? If not, type 'skip' to proceed."*
   - **If `/memory/knowledgebase/` is empty or doesn't exist:** Ask the user to provide materials directly, or skip to proceed with web research.

If none are provided, ask: *"Can you share any existing materials about your product or the competitors you want to cover? Even rough notes help. I'll fill gaps with web research."*

If the user provides a list of competitors but no materials, proceed using web search alone.

---

## Workflow

### Step 1 — Identify Competitors
Extract or ask for the list of competitors to cover. If not specified, infer from the input materials or ask: *"Which competitors should I build battlecards for?"*

### Step 2 — Extract Internal Knowledge
Read all provided inputs and extract:
- Your product's positioning, key differentiators, and proof points
- Any existing competitive intelligence (objections, win/loss notes, landmine questions)
- Customer case studies or win stories

### Step 3 — Research Each Competitor
For each competitor, use web search to enrich what's missing:
- Search `[competitor name] product positioning`
- Search `[competitor name] vs [your product]`
- Search `[competitor name] pricing` if relevant
- Search `[competitor name] customers` or case studies

Prioritize internal inputs over web search. Use search only to fill gaps or validate.

### Step 4 — Generate One Battlecard Per Competitor
Output one markdown file per competitor using the template in `assets/battlecard-template.md`.

Name each file: `battlecard-[competitor-name].md`

### Step 5 — Summarize
After generating all battlecards, provide a brief summary:
- Number of battlecards created
- Confidence level for each (High / Medium / Low) based on how much source material was available
- Gaps that still need human input (e.g. missing win stories, unconfirmed pricing)

---

## Quality Standards

- Write for a **new sales hire** — assume no prior product knowledge
- Keep language direct and conversational, not corporate
- Landmine questions should be subtle and framed as discovery questions, not attacks
- Proof points must be grounded in provided materials — do not fabricate customer names or metrics
- If a section cannot be completed confidently, mark it `⚠️ Needs input` rather than guessing

---

## Reference Files

- `references/battlecard-guidance.md` — detailed guidance on writing each section well
- `assets/battlecard-template.md` — the output template Claude fills in for each competitor
