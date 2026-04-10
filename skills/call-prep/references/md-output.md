# Call Plan — Markdown Output Instructions

Write the call plan directly as a Markdown file. Use standard GitHub-flavoured Markdown.

---

## File Location & Naming

Save the file to:

```
output/call-plan/call-plan-[company-name-lowercase-hyphenated]-[stage]-[YYYY-MM-DD].md
```

Example: `output/call-plan/call-plan-acme-corp-discovery-2026-03-10.md`

Create the `output/call-plan/` directory if it does not already exist.

---

## Document Structure

Generate the following sections in order:

### 1. Header Block

```markdown
# Call Plan — [Prospect Name] @ [Company Name]

**Role:** [Prospect Role]  
**Call Stage:** [Stage]  
**Date:** [YYYY-MM-DD]
```

---

### 2. Pre-Call Hypothesis

```markdown
## 💡 Hypothesis Going In

> [Personalised hypothesis statement]

*Write this down. You'll test it in the first 5 minutes.*
```

---

### 3. Company Research Summary

```markdown
## About [Company Name]

- [Fact 1 — size, industry, business model]
- [Fact 2 — recent news or trigger event] ⚡
- [Fact 3 — relevant tech stack or tool usage]
- [Fact 4 — relevant persona priorities]
- [Fact 5 — any other pertinent finding]
```

Flag trigger events with ⚡ inline.

---

### 4. Call Structure Sections

For each part of the call (based on the stage in `references/call-structures.md`):

```markdown
---

## PART [N] — [PART NAME] ([X] min)

*Purpose: [one-line objective for this part of the call]*

### Talk Track / Opening

> [Script or opening lines the rep will say — use blockquote for rep speech]

### Discovery Questions

- [Question 1]
- [Question 2]
- [Question 3]

### Coaching Notes

**Why this works:** [Brief rationale]
```

---

### 5. Pain-to-Demo Mapping Table (Demo stage only)

```markdown
## Pain-to-Demo Mapping

| If they said… | Show this… |
|---|---|
| [Pain statement] | [Demo moment or feature] |
| [Pain statement] | [Demo moment or feature] |
```

---

### 6. Objection Responses

```markdown
## Objection Responses

**"[Objection]"**  
[Response in natural, conversational language]

---

**"[Objection]"**  
[Response]
```

---

### 7. Success Criteria

```markdown
## ✅ Success Criteria for This Call

- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] [Criterion 3]
```

Use `- [ ]` checkbox syntax so the rep can tick items off.

---

### 8. Research Gaps (if any)

Only include this section if gaps exist.

```markdown
## ⚠️ Gaps to Confirm Before the Call

- [Gap 1 — what's unknown and why it matters]
- [Gap 2]
```

---

## Formatting Rules

- Use `##` for top-level sections and `###` for subsections
- Use `>` blockquotes for rep talk tracks and scripts
- Use `- [ ]` checkboxes in Success Criteria
- Use `⚡` to flag trigger events inline
- Use `---` horizontal rules to visually separate major sections
- Fill every section with specifics — no generic placeholders
- Mark anything uncertain as `⚠️ Research gap — confirm before call`
