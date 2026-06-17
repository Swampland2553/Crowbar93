---
name: "pdf"
description: "Use when tasks involve reading, creating, or reviewing PDF files where rendering and layout matter; verify PDF tooling before use, prefer visual checks by rendering pages with Poppler, and use Python tools such as reportlab, pdfplumber, and pypdf for generation and extraction."
source: "https://github.com/openai/skills/blob/main/skills/.curated/pdf/SKILL.md"
adapted_for: "portable Linux use"
---

# PDF Skill

## Expected dependencies

Expected tools and libraries:
- `pdftoppm` from Poppler for rendering PDF pages to PNG.
- `python3` for PDF scripts and verification.
- Python packages: `reportlab`, `pdfplumber`, `pypdf`.

Do not assume these dependencies are installed. Verify them on the current machine before use.

## When to use

- Read or review PDF content where layout and visuals matter.
- Create PDFs programmatically with reliable formatting.
- Validate final rendering before delivery.

## Workflow

1. Verify expected dependencies before first use in a new environment.
2. Prefer visual review: render PDF pages to PNGs and inspect them.
   - Use `pdftoppm` if available.
   - If unavailable, ask the user before installing system packages with `sudo`.
3. Use `reportlab` to generate PDFs when creating new documents.
4. Use `pdfplumber` or `pypdf` for text extraction and quick checks.
   - Do not rely on text extraction for layout fidelity.
5. After each meaningful update, re-render pages and verify alignment, spacing, and legibility.

## Temp and output conventions

- Use `tmp/pdfs/` for intermediate files; delete when done.
- Write final artifacts under `output/pdf/` when working in a repo.
- Keep filenames stable and descriptive.

## Verify dependencies

Check tools:

```bash
command -v pdftoppm
command -v python3
```

Check Python packages and versions:

```bash
python3 - <<'PY'
import importlib.metadata as m

missing = []
for name in ["reportlab", "pdfplumber", "pypdf"]:
    try:
        print(f"{name} {m.version(name)}")
    except m.PackageNotFoundError:
        missing.append(name)

if missing:
    raise SystemExit("missing: " + ", ".join(missing))
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

## Install missing dependencies

Ask the user before installing system-level packages or using `sudo`.

Python packages, preferred when `uv` is available and system Python install is intended:

```bash
uv pip install --system reportlab pdfplumber pypdf
```

Python package fallback:

```bash
python3 -m pip install reportlab pdfplumber pypdf
```

Fedora Poppler tools, only after user approval:

```bash
sudo dnf install -y poppler-utils
```

Ubuntu/Debian Poppler tools, only after user approval:

```bash
sudo apt-get install -y poppler-utils
```

macOS Poppler tools:

```bash
brew install poppler
```

If installation is not possible in the environment, tell the user exactly which dependency is missing and how to install it locally.

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
