# Contributing to PositioningHQ

Thank you for your interest in contributing! PositioningHQ is a Claude Code plugin with a collection of GTM and positioning skills. Contributions that improve existing skills or add new ones are very welcome.

---

## Ways to Contribute

- **Bug fixes** — A skill step is unclear, produces wrong output, or references a file that doesn't exist
- **Skill improvements** — Better prompts, more detailed asset files, improved quality standards
- **New skills** — A new GTM workflow that fits the plugin's scope (positioning, sales enablement, go-to-market, competitive intelligence)
- **Documentation** — Clearer README, better examples, additional guidance in reference files

---

## Skill Structure

Each skill lives in the `skills/` folder and follows this structure:

```
skills/
└── skill-name/
    ├── SKILL.md              # Main skill file (required) — YAML frontmatter + instructions
    ├── assets/               # Prompt fragments, templates, step-by-step guides
    │   └── *.md
    └── references/           # Supporting reference material Claude reads
        └── *.md
```

### SKILL.md Frontmatter

Every `SKILL.md` must have valid YAML frontmatter:

```yaml
---
name: skill-name         # kebab-case, matches folder name
description: One sentence describing when to use this skill.
---
```

---

## Submitting a Pull Request

1. **Fork** the repo and create a feature branch: `git checkout -b skill/my-new-skill`
2. Add your skill folder under `skills/my-new-skill/` following the structure above
3. Add your skill to `claude-plugin.json` with the path `skills/my-new-skill/SKILL.md`
4. Update the skills table in `README.md`
5. Open a PR against `main` — fill in the PR template

---

## Code of Conduct

Be constructive. Critique skill quality and output, not contributors.
