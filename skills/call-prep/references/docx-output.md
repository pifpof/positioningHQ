# Call Plan — Word Doc Output Instructions

Use the `docx` npm library to generate the call plan as a `.docx` file. Follow the instructions in the docx skill exactly.

---

## Document Setup

```javascript
const { Document, Packer, Paragraph, TextRun, Table, TableRow, TableCell,
        HeadingLevel, AlignmentType, BorderStyle, WidthType, ShadingType,
        LevelFormat } = require('docx');
const fs = require('fs');
```

Page size: US Letter (12240 x 15840 DXA), 1-inch margins (1440 DXA each side).

---

## Colour Palette

| Element | Hex |
|---|---|
| Primary accent (headings, table headers) | `1F4E79` (dark navy) |
| Secondary accent (section dividers) | `2E75B6` (mid blue) |
| Alert / warning highlight | `FF0000` |
| Table header background | `D5E8F0` |
| Body text | `000000` |

---

## Document Structure

Generate the following sections in order:

### 1. Header Block
- **Document title:** "Call Plan" — Heading 1, bold, navy
- **Metadata row:** Prospect name | Company | Role | Call Stage | Date — normal text, grey, single line

### 2. Pre-Call Hypothesis Box
A lightly shaded table (single cell, full width, `D5E8F0` background) containing:
- Label: **"Hypothesis going in:"** bold
- The personalised hypothesis statement in italics
- Sub-label: *"Write this down. You'll test it in the first 5 minutes."* in small grey text

### 3. Company Research Summary
- Heading 2: "About [Company Name]"
- 3–5 bullet points from web research: size, industry, recent news, trigger events, tech stack
- Flag trigger events in bold

### 4. Call Structure Sections
For each part of the call (based on the stage selected):
- **Part heading:** e.g. "PART 1 — SET THE STAGE (5 min)" — Heading 2, navy
- **Purpose line:** italic, grey — e.g. *Purpose: Establish credibility, set the agenda, give them control.*
- Body content: scripts, questions, coaching notes

**Scripts and talk tracks:** render in a lightly bordered box (single-cell table, `F5F5F5` background) with italic text. This visually distinguishes what the rep says from coaching notes.

**Discovery questions:** render as a bulleted list

**Coaching notes** (e.g. "Why this works:"): render in normal body text, preceded by a bold label

### 5. Pain-to-Demo Mapping Table (Demo stage only)
Two-column table: "If they said…" | "Show this…"
- Header row: `1F4E79` background, white bold text
- Body rows: alternating white / `F0F4F8`

### 6. Objection Responses
- Heading 2: "Objection Responses"
- For each objection: bold italic objection text, then response in normal text below
- Separate each objection with a thin rule (paragraph bottom border)

### 7. Success Criteria
- Heading 2: "Success Criteria for This Call"
- Bulleted checklist items
- Add a checkbox character `☐` before each item for the rep to use on the day

### 8. Research Gaps (if any)
- Heading 2: "⚠️ Gaps to Confirm Before the Call"
- Bulleted list of anything marked as uncertain or needing human input
- Only include this section if gaps exist

---

## Formatting Rules

- **Never use `\n`** — use separate Paragraph elements
- **Never use unicode bullets** — use `LevelFormat.BULLET` with numbering config
- **Tables:** always set `columnWidths` AND cell `width`, both in DXA, summing to 9360
- **Shading:** always use `ShadingType.CLEAR`, never SOLID
- **Cell padding:** `margins: { top: 80, bottom: 80, left: 120, right: 120 }`
- **Script boxes:** single-cell table, `F5F5F5` background, `CCCCCC` border, italic TextRun

---

## File Naming

`call-plan-[company-name-lowercase-hyphenated]-[stage]-[YYYY-MM-DD].docx`

Example: `call-plan-acme-corp-discovery-2026-03-10.docx`

---

## Validation

After generating, run:
```bash
python scripts/office/validate.py [filename].docx
```

If validation fails, unpack the XML, fix, and repack.
