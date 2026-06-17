---
name: "pdf"
description: "Use when tasks involve reading, creating, or reviewing PDF files where rendering and layout matter; prefer visual checks by rendering pages with Poppler and use Python tools such as reportlab, pdfplumber, and pypdf for generation and extraction."
source: "https://github.com/openai/skills/blob/main/skills/.curated/pdf/SKILL.md"
adapted_for: "/root/gg4 on 2026-06-17"
---

# PDF Skill

## Local machine status

This file is adapted for this machine.

Available here:
- `pdftoppm`: `/usr/bin/pdftoppm` (Poppler 25.07.0)
- `uv`: `/usr/bin/uv` (0.11.15)
- `python3`: `/usr/bin/python3` (3.14.5)
- `pip`: `/usr/bin/pip` (25.1.1)
- `npx`: `/usr/bin/npx` (10.9.7)

Python packages installed in system Python:
- `reportlab` 4.5.1
- `pdfplumber` 0.11.10
- `pypdf` 6.13.3

Not available here:
- Global `skills` CLI
- `brew`
- `apt-get`

## Skill installation

The global `skills` command is not installed on this machine.

Use `npx` if installing this skill into a skills-aware environment:

```bash
npx skills add https://github.com/openai/skills --skill pdf
```

Global `skills` CLI is not required for using the PDF tooling already installed here.

## When to use

- Read or review PDF content where layout and visuals matter.
- Create PDFs programmatically with reliable formatting.
- Validate final rendering before delivery.

## Workflow

1. Prefer visual review: render PDF pages to PNGs and inspect them.
   - Use `pdftoppm`; it is already available on this machine.
2. Use `reportlab` to generate PDFs when creating new documents.
3. Use `pdfplumber` or `pypdf` for text extraction and quick checks.
   - Do not rely on text extraction for layout fidelity.
4. After each meaningful update, re-render pages and verify alignment, spacing, and legibility.

## Temp and output conventions

- Use `tmp/pdfs/` for intermediate files; delete when done.
- Write final artifacts under `output/pdf/` when working in this repo.
- Keep filenames stable and descriptive.

## Dependencies

Dependencies are already installed on this machine.

If they need repair or reinstall, use system Python with `uv`:

```bash
uv pip install --system reportlab pdfplumber pypdf
```

Fallback if `uv` becomes unavailable:

```bash
python3 -m pip install reportlab pdfplumber pypdf
```

Do not use these source-file commands on this machine:

```bash
brew install poppler
sudo apt-get install -y poppler-utils
```

Reason: `brew` and `apt-get` are not available here. Poppler rendering is already available through `pdftoppm`.

## Environment

No required environment variables.

## Rendering command

```bash
pdftoppm -png "$INPUT_PDF" "$OUTPUT_PREFIX"
```

Example:

```bash
mkdir -p tmp/pdfs/rendered
pdftoppm -png input.pdf tmp/pdfs/rendered/page
```

## Quick verification

Check installed Python packages:

```bash
python3 - <<'PY'
import importlib.metadata as m
for name in ["reportlab", "pdfplumber", "pypdf"]:
    print(name, m.version(name))
PY
```

Check imports:

```bash
python3 - <<'PY'
import reportlab, pdfplumber, pypdf
print("imports ok")
PY
```

Check renderer:

```bash
pdftoppm -v
```

## Quality expectations

- Maintain polished visual design: consistent typography, spacing, margins, and section hierarchy.
- Avoid rendering issues: clipped text, overlapping elements, broken tables, black squares, or unreadable glyphs.
- Charts, tables, and images must be sharp, aligned, and clearly labeled.
- Use ASCII hyphens only. Avoid Unicode dashes in generated PDFs.
- Citations and references must be human-readable; never leave tool tokens or placeholder strings.

## Final checks

- Do not deliver until latest PNG inspection shows zero visual or formatting defects.
- Confirm headers, footers, page numbering, and section transitions look correct.
- Keep intermediate files organized or remove them after final approval.
