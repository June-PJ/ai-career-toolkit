---
name: resume-publisher
description: Use when converting a finalized Markdown resume into a polished DOCX file for job applications, especially when the user asks to format, export, publish, typeset, or prepare a resume for submission.
---

# Resume Publisher

## Overview

Turn a reviewed Markdown resume into a clean, ATS-friendly Word DOCX deliverable. Treat the Markdown file as the source of truth; do not rewrite facts or inflate claims unless the user explicitly asks for content edits.

## Workflow

1. Read the Markdown resume and identify the target role, name, contact block, sections, project entries, and bullets.
2. Run the delivery checklist in `references/delivery_checklist.md`.
3. Apply the layout rules in `references/resume_layout_rules.md`.
4. Generate DOCX with `scripts/build_resume_docx.py`.
5. Inspect the final document visually before saying it is ready to submit.

## Quick Start

Use the script from the skill directory:

```bash
python scripts/build_resume_docx.py path/to/resume.md --outdir path/to/output
```

Optional flags:

```bash
python scripts/build_resume_docx.py resume.md --basename "姓名-岗位方向"
python scripts/build_resume_docx.py resume.md --photo path/to/headshot.jpg
```

The skill generates DOCX only. Any later format conversion should be handled outside this skill.

## Output Contract

Create one file:

- `<姓名>-<岗位方向>.docx`

Use the DOCX as the editable deliverable. Keep the source Markdown unchanged unless the user asks for resume content edits.

## Publishing Rules

- Prefer one to two pages for early-career technical resumes.
- Use simple typography, clear section headings, compact spacing, and real text.
- Do not use skill bars, radar charts, decorative icons, or image-only resume layouts.
- Do not add a headshot by default for technical/ATS-oriented submissions. Add one only when the employer expects it, the platform asks for it, or the user explicitly requests it.
- Do not add metrics, tools, titles, or project scope that are not present in the source or confirmed by the user.
- Remove Markdown-only artifacts from the deliverable, including horizontal rules, raw `#`, raw `**`, and code fences.
- Keep links as visible text when they are useful for ATS parsing.

## Common Mistakes

| Mistake | Fix |
|---|---|
| Rewriting the resume while exporting | Only format unless content editing is requested. |
| Making a flashy visual template | Use ATS-friendly text layout. |
| Shipping DOCX without visual review | Render or open-check the document first. |
| Trying to automate non-DOCX export from the skill | Generate DOCX only. |
| Letting Chinese text use random fallback fonts | Set explicit CJK fonts in styles. |
