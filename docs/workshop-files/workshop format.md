# Positioning Playbook Workshop — Full Format Guide (v3)
> Facilitator and participant reference. For use in Lightship sessions and Imad's sales/marketing/enablement team workshop.

---

## Overview

This workshop teaches participants two things simultaneously: how modern AI systems actually work, and how to build a world-class positioning playbook for their company using those systems. The learning is embedded in the doing — by the time participants leave, they have a real deliverable and a real mental model.

**Who this is for:**
- Founders and revenue leaders who want clear, differentiated positioning
- Sales and marketing teams who need a shared language and toolkit
- Any team that currently has inconsistent messaging across decks, reps, and emails

**What participants leave with:**
- A complete Positioning Playbook for their company
- Competitive battlecards ready for sales
- A personalized call prep tool they can use before any deal
- A working understanding of how to use Claude as an AI system — not just a chatbot

**Workshop duration:** Half-day (3–4 hours) or split across two sessions

---

## Chapter 1 — Understanding The Fundamentals

> *Purpose: Before we build anything, we need a shared mental model of what AI systems actually are and how they work. This isn't theory — every concept here directly explains something you'll use in the workshop.*

---

### 1.1 LLMs vs. Chatbots

Most people think of AI as a chatbot — a smart autocomplete that answers questions. That's not what we're working with.

A **Large Language Model (LLM)** is a trained reasoning engine. It has internalized vast amounts of human knowledge and can understand context, follow instructions, generate structured outputs, and reason across complex problems. Claude, GPT-4, and Gemini are all LLMs.

A **chatbot** is an interface layer — a way of talking to a system. The underlying intelligence can be very simple (scripted responses) or very powerful (an LLM). Most corporate chatbots are scripted. Claude is not.

The critical distinction for this workshop: **an LLM can be given a role, a context, a set of instructions, and a memory — and it will behave like a specialist collaborator, not a search engine.** That's what we're building with.

Think of it this way: using ChatGPT as a chatbot is like hiring a brilliant consultant and only ever asking them to write emails. In this workshop, we're going to give that consultant a proper brief, relevant context, and a structured process — and watch what they actually produce.

---

### 1.2 RAG, Context Windows, and When Each Applies

To understand how we're architecting the PositioningHQ system, you need to understand two approaches to giving AI models external knowledge.

**RAG (Retrieval-Augmented Generation)** stores documents in a vector database, then retrieves the most relevant chunks at query time and injects them into the model's context. When you ask a question, the system doesn't load everything — it searches for and retrieves only what's relevant. RAG is the right architecture when you have large, dynamic document sets: a company's entire knowledge base, a CRM with thousands of records, a product documentation library with hundreds of files.

**Large context windows** take a different approach: instead of retrieving selectively, you include all relevant documents directly in the model's input. Claude's context window holds up to 200,000 tokens — roughly the equivalent of one to two full novels, or several hundred pages of dense business documents. For a bounded, known set of files, you can simply load them all and the model reads them in full.

**For this workshop, we use the large context approach — and here's why that's the right call for this specific use case:**

Your company's positioning context is bounded and small. A few input files describing your product, customers, and market might total 5,000–10,000 tokens. Loading these directly in the right format is simpler, cheaper, and sufficient. No database infrastructure needed.

However, it's worth being precise about what context windows have and haven't changed. They have simplified architecture for small, bounded datasets like this one. They have not made RAG obsolete as a general pattern. At scale — enterprise knowledge bases, large CRM datasets, real-time data retrieval — RAG remains the right approach for three concrete reasons:

1. **Cost efficiency**: Processing 200K tokens on every query is expensive. RAG retrieves only the relevant chunks, dramatically reducing inference costs.
2. **The "lost in the middle" problem**: Research by Liu et al. (2023) demonstrated empirically that LLMs reliably process content at the beginning and end of long contexts, but underperform on information buried in the middle. Larger context does not mean perfectly uniform attention.
3. **Dynamic data**: A context window holds what you load at the start of a session. RAG can retrieve from live databases, CRMs, and APIs where the data changes continuously.

**The takeaway:** Choose the approach that fits your data. For this workshop — a small, structured set of company files — context + Markdown is the right answer. For enterprise-scale systems, RAG remains essential.

---

### 1.3 Markdown — The Native Language of AI Systems

Markdown is a plain-text formatting system that uses simple symbols to indicate structure: `#` for headings, `**text**` for bold, `-` for lists, `|` for tables.

It has become the de facto standard for AI-facing content for three reasons:

**Density.** Markdown packs semantic structure into minimal tokens. A well-formatted Markdown document communicates hierarchy, relationships, and emphasis more clearly than an equivalent Word doc — with less noise.

**No formatting overhead.** When you give an AI a Word document or PDF, the model must interpret layout artifacts, footers, fonts, and formatting metadata. Markdown is plain text — what you write is what the model processes, with no structural noise.

**File system compatible.** Markdown files are just `.md` text files. They live in folders, work with version control, load instantly, and can be written or updated programmatically by the AI itself. This makes them ideal for the memory architecture we'll use in this workshop.

**Practical rule for this workshop:** When writing context for Claude — company background, product details, customer profiles — write it in Markdown. Structured, dense, organized. Not prose paragraphs buried in slide decks, not tables locked in spreadsheets.

---

### 1.4 The Problem with Long-Running Chat Threads

Here is something that surprises most people: **Claude does not have persistent memory between conversations.** Each new conversation starts fresh. And within a long conversation, problems accumulate.

Two distinct things go wrong in long threads:

**The "lost in the middle" problem.** When a context window fills up with a long conversation, the model processes all of it — but research shows models reliably attend to content at the beginning and end of the sequence, and statistically underutilize content buried in the middle. Long threads mean important instructions get pushed to the middle. The result: inconsistent behaviour that feels random but follows a pattern.

**Instruction drift.** As conversations grow, later messages can functionally dilute the influence of earlier instructions. The model optimises for recent context. A system prompt written at the start loses relative influence as the thread grows. This is why long sessions with Claude can feel like the model has "forgotten" what you asked it to do.

The practical consequences:
- Outputs become less consistent as the thread grows longer
- Sessions aren't resumable — if you close the app, the context is gone
- Different team members can't share the same session state
- Every new session means re-briefing from scratch

**The solution is a memory architecture built on files** — which brings us to the next concept.

---

### 1.5 Memory Systems Built on Markdown Files and Folders

Instead of relying on chat history, we store everything the AI needs to know in structured files. The model reads these files at the start of each session and has full context instantly — regardless of which session, which machine, or which team member opens it.

This is the architecture behind the PositioningHQ skill pack:

```
your-company/
├── inputs/           ← What you tell the AI about your company
│   ├── company.md    ← Overview, mission, product description
│   ├── icp.md        ← Who your customers are
│   └── positioning.md ← Draft positioning (gets overwritten by the playbook)
├── memory/           ← What the AI builds and remembers
│   ├── research/     ← Market and competitive research
│   └── playbook/     ← The finished positioning playbook
└── outputs/          ← Deliverables
    ├── battlecards/  ← One per competitor
    └── call-plans/   ← One per deal
```

The model never has to be re-briefed. Open Claude, run the skill, and it knows exactly where to look. The outputs persist across sessions. Multiple team members can access the same vault. The system compounds over time.

**The shift in mindset:** Stop thinking of AI as a chat session. Start thinking of it as a team member with a well-organized desk.

---

### 1.6 Skills, Agents, and MCP

Three terms that matter as you work with Claude at a professional level:

**Skills** are packaged instruction sets — structured prompts with embedded logic that tell Claude how to approach a specific task. When you run `/positioning-playbook`, you're invoking a skill. It loads a set of instructions, follows a defined process, and produces a structured output. Skills are repeatable, shareable, and improvable over time. Think of them as SOPs for your AI collaborator.

**Agents** are AI systems configured to take actions and operate autonomously across multiple steps, using tools and file access to accomplish goals without you guiding each step. The `/setup-positioning-vault` skill in this workshop behaves agentically — it reads your inputs, runs web research, builds a playbook, and writes output files in sequence. You start it and come back to results.

**MCP (Model Context Protocol)** is an open standard developed by Anthropic for connecting AI models to external tools and data sources. MCP lets Claude interact with your calendar, CRM, code repository, Slack, or any system you connect. The protocol is open and increasingly supported by third-party tools. For this workshop, you don't need to configure any MCP servers — but understanding the architecture shows where this scales.

**The mental model:** Skills are the SOPs, agents are the autonomous workers, MCP is the plumbing that connects them to your real systems.

---

### 1.7 Claude Desktop, Claude Code, and Cowork

Three ways to access Claude that matter for this workshop:

**Claude.ai** is the browser interface — useful for quick tasks, but has no persistent file system access and no plugin support. Not where we'll work today.

**Claude Desktop** is the Mac/PC application. It supports plugins (installed skill packs), can access files on your machine via a connected workspace folder, and integrates with MCP servers. This is what participants use today.

**Claude Code** is the terminal-based interface for developers. It runs directly in your working directory, has full file system and shell access, and is designed for technical users building and deploying systems. The PositioningHQ plugin was built using Claude Code.

**Cowork** is Anthropic's interface for non-developer users within the Claude desktop application — a structured workspace designed to make AI workflows accessible without a command line. Parallel79° builds the skills, plugins, and workflows that run inside it. That distinction matters: Anthropic provides the platform; what you're using today is a Parallel79° plugin running on top of it.

**For this workshop:** Participants use Claude Desktop. If you're on a computer without a terminal and you're using the Cowork-style interface, the workflow is identical — you're still running the same plugin commands.

---

### Chapter 1 Conclusion

You now have the mental model: Claude is a reasoning engine, not a chatbot. We give it structured context through Markdown files, persist its work through a file-based memory system, and give it skills to follow repeatable processes. Long chat threads are replaced by organized vaults. The architecture is simple — by design.

Everything you build today — the research, the playbook, the battlecards — lives in your vault. The system gets more useful with every session.

---

## Chapter 2 — Setting Up Your Claude Desktop Environment

> *Purpose: Get every participant running before we start building. This should take 15–20 minutes.*

---

### 2.1 What You Need

- A Mac or Windows computer
- A paid Claude subscription — check [claude.ai](https://claude.ai) for current plans and confirm which tier includes plugin support in Claude Desktop
- The PositioningHQ plugin (provided by workshop facilitator or installed via the command below)

---

### 2.2 Install Claude Desktop

1. Go to [claude.ai/download](https://claude.ai/download) and download the desktop app for your OS
2. Sign in with your Claude account (same credentials as claude.ai)
3. Confirm you're on a plan that supports plugins — look for the model selector and plugin management in settings

---

### 2.3 Install the PositioningHQ Plugin

The facilitator will provide an installation command. Once installed:

1. Open Claude Desktop and start a new conversation
2. Type `/` — the PositioningHQ skills should appear in the autocomplete list
3. Confirm the following commands are available:
   - `/setup-positioning-vault`
   - `/company-research`
   - `/positioning-playbook`
   - `/battlecard`
   - `/call-plan`
   - `/product-launch`

If commands aren't showing, restart Claude Desktop and try again. If the plugin isn't loading, confirm your subscription supports it.

---

### 2.4 Choose Your Working Directory

Claude Desktop needs file system access to read and write your vault. Before running any skills:

1. In Claude Desktop, connect a workspace folder — this is the directory where your vault will live (e.g., `~/Documents/PositioningHQ/YourCompany`)
2. Create this folder on your computer first if it doesn't exist
3. Connect it via the workspace/folder control in Claude Desktop

Everything the skills produce will be written into this folder. This is your vault. Keep it somewhere you can access from other tools and share with teammates.

---

### 2.5 Prepare Your Company Brief

Before running the setup skill, it helps to have a rough brief ready. A few paragraphs covering:
- What your company does and who it's for
- The problem you solve and how you're different
- Your typical customer (size, industry, role)
- 2–3 competitors you know about
- Gather all relevant sales,  marketing, and enablement documents such as pitch decks, FAQ, objection handling, customer testimonials, etc. 

This doesn't need to be polished. The AI will research and structure everything — you're giving it a starting point. If you don't have any formal documents, quick notes, a voice memo transcription, or a rough bullet list all work. These will be asked as input to inform the preparation of your positioning draft. 

---

## Chapter 3 — The Positioning Framework

> *Purpose: Before using the tools, participants need to understand what they're building and why. This chapter covers the philosophy and the framework structure.*

---

### 3.1 What Positioning Actually Is

Positioning has a precise meaning that most companies misunderstand.

> **"Positioning defines how your product is a leader at delivering something that a well-defined set of customers cares a lot about."** -- April Dunford

Notice what that definition is not about: your product's features, your technology stack, your founding story, or your roadmap. It's about customers — specifically, a *defined* set of them and what they *genuinely care about*.

This is the most common positioning mistake: building messaging around what you built instead of what your customers are trying to accomplish. Features get copied. Customer understanding is a moat.

**Product positioning is about our customers, not our product.** It's about who they are and why they care — not what we can do for them.

---

### 3.2 The Guide Mindset

The positioning philosophy that underpins this framework is borrowed from narrative strategy: **your customers are the heroes. You are the guide.**

They are Batman. You are Alfred. They are trying to accomplish something that matters to them — grow revenue, reduce risk, save time, win a market. Your job is not to make them care about your product. It's to show them that you understand their mission and that you have what they need to complete it.

This changes everything about how you position:

- You don't talk *at* them about you. You **show empathy** — demonstrate that you understand who they are, what they're trying to do, the outcome they want, and how painful it is to not get there.
- You **demonstrate expertise** — show you've done this before (proof), that you know what it takes (value statements), that you have a way of doing it (your solution), and that your way is better than the alternatives (distinct differentiation).

The framework is built around making both of these things explicit and structured.

---

### 3.3 The Framework Structure

The Product Positioning Playbook Framework has seven elements, organized around a central insight: your solution exists inside a customer context, and everything you say must be grounded in that context.

**The two sides of the framework:**
- **Customer Context (elements 1–5)** — who they are, what's happening in their market, what they care about, and who you're up against
- **Your Solution + Proof (elements 6–7)** — how your solution is positioned inside that context, and the evidence that backs it up

**The seven elements:**

**01. Market Overview — The "Why Now?"** — What is happening in the market that makes this solution necessary at this moment? What are the shifts, the windows, the inflection points? This is the cross-functional source of truth that keeps product, marketing, and sales aligned on market reality. Without a compelling "why now," even great positioning falls flat.

**02. Target Customers & ICP** — The demographic and characteristic definition of your right-fit customer. Company size, industry, geography, revenue stage, buying triggers. This goes beyond a demographic profile — it includes who the economic buyer is, who the daily user is, and who influences the decision. The ICP is not a wish list — it's a precise description of the customer for whom you win, reliably.

**03. Value Drivers** — The three outcomes your ideal customers find genuinely valuable. Not features — outcomes. For each value driver: the customer challenge, the status quo (how they handle it today), the cost of inaction, your distinct advantage, the future state, proof points, and the discovery questions that help buyers surface this pain themselves.

**04. Distinct Advantages (Moat)** — How you do it differently and better than anyone else for your target customers. The specific capabilities, approaches, or assets that you have and competitors don't — and that your ICP actually cares about. Differentiators that nobody cares about aren't differentiators. Differentiators that everyone has aren't distinctive. The overlap between "genuinely unique" and "genuinely valued" is the moat.

**05. Competitive Intelligence** — Deep, up-to-date knowledge of your competitive landscape. How each competitor positions themselves, where they're strong, where they're vulnerable, and how to win against them in a live deal. This element keeps the playbook honest — positioning that ignores competitive reality doesn't survive first contact with a buyer.

**06. Positioning Your Solution** — How your solution is a leader at delivering something that a well-defined set of customers cares a lot about. (April Dunford's definition is the right anchor here.) This is where everything comes together: your solution positioned inside the customer's context, not in front of it. How you do it, how you do it differently, how you do it better than the alternatives, and what happens if the customer doesn't act.

**07. Proof Points** — The evidence behind every claim in the playbook. Customer case studies, testimonials, analyst reports, win stories, quantified outcomes. Proof Points are what separate a positioning statement from a marketing claim. Without them, elements 3–6 are assertions. With them, they're facts.

---

### 3.4 What You Build With It

The Positioning Playbook is a **Value Framework Document** — the internal source of truth that aligns product, marketing, and sales on three things:

**Accelerate Revenue Growth Reliably** — ensures sales and CX teams are constantly going after the right accounts with the right message.

**Consistent Messaging** — drives consistency from top-of-funnel through expansion. Every rep, every email, every deck starts from the same foundation.

**Alignment** — connects product strategy to go-to-market plan, revenue teams to product team, and customer requests to the product roadmap. No more "marketing says one thing, the product does another."

**Building on the outcome** — once the playbook exists, it powers everything downstream: brand story and website copy, employee onboarding and sales enablement programs, and product strategy alignment to deliver the value you've promised.

---

## Chapter 4 — Building Your Positioning Playbook with Claude

> *Purpose: Hands-on section. Participants run the skills against their own company. The facilitator walks through each step.*

---

### 4.1 The Workflow Overview

The PositioningHQ skill pack follows a deliberate sequence. You don't need to run every skill — but the order matters:

```
/setup-positioning-vault
        ↓
  (auto-runs /company-research + /positioning-playbook)
        ↓
/battlecard      /call-plan      /product-launch
```

The setup skill is the entry point. It creates your vault structure, collects your company context through a guided interview, and automatically runs research and playbook generation. By the time it's done, you have a vault with research and a first-draft playbook.

---

### 4.2 Step 1 — Run `/setup-positioning-vault`

Type `/setup-positioning-vault` and press Enter.

Claude will walk you through a structured intake. Expect questions about:
- Your company name, website, and a brief description of what you do
- Your target market and the customers you serve best
- The specific problem you solve and the alternatives you compete with
- Any internal documents you want to use as source material (pitch deck, existing positioning docs, case studies)

**Tips for this step:**
- Answer with specificity. "Mid-sized SaaS companies" is less useful than "50–200 person SaaS companies in North America with a dedicated sales team and a product-led growth motion." The more specific your input, the stronger the output.
- Share your pitch deck or existing sales materials if you have them. Claude will extract relevant content and weave it into the playbook.
- If you don't have materials, type "skip" and Claude will proceed with web research.

After the intake, Claude will automatically run `/company-research` and then `/positioning-playbook`. This takes 5–10 minutes. Let it run.

---

### 4.3 What `/company-research` Produces

The research skill runs a 9-step market and competitive analysis:

1. Company overview and business model
2. Product analysis — what it does, how it works
3. Market segment — TAM, growth rate, dynamics
4. Customer segment — who actually buys, what they care about
5. Strengths — real advantages, validated by evidence
6. Weaknesses — honest gaps, things competitors exploit
7. Recent developments — funding, product launches, leadership changes
8. Competitive analysis — how alternatives are positioned
9. Synthesis — "sweet spot" statement: where you win and why

This is saved to `/memory/company-research/` in your vault. The positioning playbook skill reads it automatically — you don't need to copy and paste anything.

---

### 4.4 What `/positioning-playbook` Produces

The playbook skill reads your research and builds a complete 7-section Positioning Playbook:

**Section 1 — Market Overview ("Why Now?"):** A dense explanation of market necessity, plus a Trends & Shifts table showing 3–4 inflection points and the windows of opportunity each creates, plus a Landscape Map showing how you fit against alternatives.

**Section 2 — Target Customers & ICP:** The ICP formula, a structured ICP table (size, industry, geography, key roles), buyer and user personas, Jobs to Be Done, a Pain vs. Gain table, Alternative Solutions comparison, and Buying Triggers.

**Section 3 — Value Drivers:** Three high-resonance business outcomes, each expanded with: customer challenge, status quo, cost of inaction, distinct advantage, future state, proof points, and 2–3 discovery "trap questions" for sales reps.

**Section 4 — Distinct Advantages (Moat):** What you have that competitors don't — and that your ICP actually cares about. How you do it differently and better than anyone else for your target customers.

**Section 5 — Competitive Intelligence:** Per-competitor breakdowns — how they position, where they're strong, where they're weak, and how to win against each one in a live deal.

**Section 6 — Positioning Your Solution:** The internal source of truth in structured table format (For / Who are dissatisfied with / Our product is / That provides / Unlike / We), plus three message variations: sales elevator pitch, investor/executive framing, and website H1/H2 copy.

**Section 7 — Proof Points:** Real evidence. Case studies, metrics, quotes, and win stories — sourced from materials you provide or flagged as needing input. These are what separate positioning claims from positioning facts.

The full playbook is saved to `/memory/positioning-playbook/` as a single professional `.md` document. This is the living source of truth — update it as the market changes.

---

### 4.5 Reviewing and Refining the Playbook

The first output is a strong draft, not a final document. After Claude completes the playbook:

1. Read through each section and note where it got something wrong or where you have stronger input to provide
2. For anything marked `⚠️ Needs input` — add the missing detail and ask Claude to regenerate that section
3. Pay particular attention to Value Drivers and Proof Points — these benefit most from human input. Claude can infer pain, but real customer language and real metrics are irreplaceable.

Expect one round of refinement for a solid v1. Most teams do 2–3 iterations over the first month as they stress-test the playbook in real conversations.

---

## Chapter 5 — Using Your Positioning Playbook

> *Purpose: The playbook is only as valuable as the workflows it enables. This chapter covers the two daily-use tools: battlecards and call plans.*

---

### 5.1 Competitive Battlecards with `/battlecard`

A battlecard is a one-page reference document that gives a sales rep everything they need to win a deal against a specific competitor. Not feature comparisons — a practical guide to the conversation in context of that specific opportunity.

Each battlecard contains:
- **Who they are** — how the competitor positions, who they target, what they're proud of
- **Where they're strong** — honest assessment, so reps aren't caught off-guard
- **Where they're weak** — the real gaps, framed for the sales conversation
- **How to win against them** — specific positioning angles and proof points
- **Landmine questions** — subtle discovery questions that help the buyer surface concerns about the competitor, framed as natural discovery rather than attacks
- **Objection handling** — the three most common things a prospect says when leaning toward the competitor, and how to respond

**Running the skill:**

Type `/battlecard` and specify which competitor(s) you want to cover. Claude will:
1. Check your vault for the positioning playbook (reads it automatically)
2. Check for any existing competitive intelligence in your knowledge base
3. Research the competitor via web search to fill gaps
4. Generate one battlecard per competitor

Battlecards are saved to `/outputs/battlecards/`. Share with your sales team as-is or copy into your existing enablement platform.

**Quality note:** Battlecards are only as good as your internal knowledge plus what's publicly available. Sections most likely to need human input: confirmed win stories and pricing. Add your real data before distributing.

---

### 5.2 Call Preparation with `/call-plan`

The call plan skill generates a personalized, stage-specific pre-call brief for any sales conversation. Not a script — a strategic briefing document.

Before running the skill, have ready:
- The prospect company name
- The name and role of the person you're meeting
- The call stage: discovery / demo / follow-up / closing
- Any relevant context: known pain points, prior conversations, their tech stack

**Running the skill:**

Type `/call-plan` and provide the above details. Claude will:
1. Research the prospect company via web search (recent news, funding, leadership changes, industry context)
2. Read your positioning playbook to load your value props, ICP, differentiators, and proof points
3. Select the appropriate call structure for the stage
4. Generate a complete, personalized call plan

Each call plan includes:
- **Opening hypothesis** — a specific, prospect-relevant statement of the problem you think they have, designed to start a real conversation
- **Discovery questions** — tied directly to your Value Drivers, ordered to build understanding progressively
- **Landmine questions** — framed to surface concerns about competitors or the status quo naturally
- **Proof points** — matched to the prospect's industry and likely situation
- **Objection handling** — the most likely pushbacks and how to address them from your positioning
- **Recommended next step** — a specific ask, not "I'll follow up"

Call plans are saved to `/outputs/call-plans/`. Most reps review it the morning of the call and bring the key questions and hypothesis into the conversation.

---

### 5.3 The Feedback Loop

The playbook improves through use. After every significant sales conversation:

- Did the discovery questions land? If not, refine the Value Drivers.
- Did a prospect use language we haven't captured? Add it to the ICP section.
- Did we win or lose on a specific competitive point? Update the battlecard.
- Did a proof point land particularly well? Elevate it to the top of that Value Driver.

This isn't a quarterly review process — it's a living document. Share your notes from a call and ask Claude to refine the relevant section of the playbook.

---

## Chapter 6 — What's Next

> *Purpose: Close the workshop with a forward-looking exercise. Participants identify the three highest-impact ways to extend what they've built today into their broader systems.*

---

### 6.1 The Exercise

Now that you have a positioning playbook, battlecards, and a call prep tool — what else should this enable?

Take 15 minutes in small groups to map your answer across three categories:

**Messaging & Content**
- Where is your messaging currently inconsistent? (website, outbound emails, social, ads)
- Which pieces of content would be most valuable to rebuild from the new playbook? (homepage, deck, email sequences, case studies)
- Who owns each of those — and what would it take to brief them with the playbook?

**Sales & Enablement**
- Which reps are most likely to use a battlecard or call plan tool today? Start there.
- What's your current new hire onboarding for positioning? How does the playbook change it?
- What's the highest-friction part of your sales process — and could better positioning fix it?

**Product & Roadmap**
- Are there commitments in your positioning that your product doesn't yet fully deliver?
- Are there customer jobs in your ICP section that you're not currently addressing?
- How does the positioning change what you prioritize on the roadmap?

---

### 6.2 Rollout Priorities

At the end of the exercise, each team should leave with three commitments:

1. **The first thing we'll update** — the single piece of messaging or collateral that would benefit most immediately from the new positioning
2. **The team we'll brief first** — the internal team (sales, CS, marketing, product) that most needs alignment right now
3. **The feedback loop we'll create** — how we'll capture what's working and what isn't, and how often we'll update the playbook

---

### 6.3 How to Continue Building

The PositioningHQ skill pack is a starting point. As your company and market evolve:

- Run `/company-research` again whenever there are significant market changes, new competitors, or major product updates
- Re-run `/positioning-playbook` when you enter a new market or target a new segment
- Add new battlecards as new competitors emerge
- Use `/product-launch` when shipping major new capabilities — it generates a launch plan including a positioning impact assessment against your existing playbook

The vault compounds. Every session adds to what Claude knows about your company. The system gets stronger with use.

---

## Appendix — Quick Reference

### Skill Commands

| Command | What it does | When to run |
|---|---|---|
| `/setup-positioning-vault` | One-time setup: creates vault, runs research + playbook | First time only |
| `/company-research <name>` | 9-step competitive and market research | When market changes significantly |
| `/positioning-playbook` | Full 7-section positioning playbook | After research, when repositioning |
| `/battlecard` | One battlecard per competitor | When entering competitive deals |
| `/call-plan` | Personalized pre-call brief | Before every significant sales call |
| `/product-launch` | Full launch plan with positioning impact | Before major product releases |

### Vault Structure

```
your-company/
├── inputs/                    ← Your company context
├── memory/
│   ├── company-research/      ← Market + competitive research
│   ├── positioning-playbook/  ← The living playbook
│   └── knowledgebase/         ← Case studies, decks, FAQs
└── outputs/
    ├── battlecards/           ← Per-competitor battlecards
    ├── call-plans/            ← Per-deal call plans
    └── launch/                ← Launch plans
```

### The Framework at a Glance

| # | Element | What it defines |
|---|---|---|
| 01 | Market Overview — The "Why Now?" | The market shifts and windows of opportunity that make your solution necessary right now |
| 02 | Target Customers & ICP | Who you win with, reliably — demographics, buyer roles, and decision dynamics |
| 03 | Value Drivers | The 3 outcomes your ICP will shift budget to achieve |
| 04 | Distinct Advantages (Moat) | How you do it differently and better than anyone else for your target customers |
| 05 | Competitive Intelligence | How competitors position, where they're weak, and how to win against them |
| 06 | Positioning Your Solution | Your solution positioned inside customer context — not in front of it |
| 07 | Proof Points | The evidence behind every claim — case studies, testimonials, win stories |

---

*This workshop was developed by Parallel79° in collaboration with PositioningHQ. The PositioningHQ framework is published under Creative Commons CC0 1.0.*
