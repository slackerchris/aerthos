# Aerthos — Worldbuilding & Book Project

This repository contains the worldbuilding, reference materials, and manuscript files for the Aerthos series (Book 1: Echo of the Sunstone). The goal is to keep facts, style rules, timelines, character notes, and build scripts in a single place so you can write consistently across a long series and easily generate exports for reviewers, editors, or readers.

This README is tailored to the files already in the repo (see `updated_project_package.md`). If you'd like I can also scaffold build scripts, templates, or a CI workflow to export PDFs or publish a docs site.

## What I found in this repository
- `updated_project_package.md` — a comprehensive project package with character guides, world reference, magic system, timelines, style guide, and many other reference sections. This is the main source of truth you already have.
- `Echo of the Sunstone.docx` — the manuscript for Book 1 in Word format.

If you have other files (images, chapter markdown, notes), add them under the folders suggested below.

## Recommended repo layout
Use a consistent layout so material is easy to find, edit, and automate:

- `manuscripts/` — working drafts and chapter files. Prefer Markdown (`.md`) for version control and automation. Example: `manuscripts/book1/*.md`.
- `world/` — split the large `updated_project_package.md` into focused reference files:
	- `world/characters.md` or `world/characters/<name>.md`
	- `world/locations.md`
	- `world/pantheon.md`
	- `world/magic.md`
	- `world/timeline.md`
	- `world/artifacts.md`
- `style/` — `style_guide.md`, character voice cheat-sheets (e.g., `style/anya.md`).
- `assets/` — images, maps, diagrams.
- `scripts/` — small utilities and build scripts (Pandoc exports, converters).
- `templates/` — Pandoc/LaTeX templates and CSS for web exports.
- `dist/` — generated artifacts (PDFs, HTML). Add to `.gitignore`.
- `.github/workflows/` — CI workflows to build and publish exports.

## Why restructure the large package file
- Easier diffs and history: smaller files show exactly what changed and when.
- Better collaboration: other contributors can edit specific parts without touching everything.
- Automation-friendly: scripts can assemble a book from chapter Markdown files and include metadata from small reference files.

## Practical next steps (priority order)
1. Convert `Echo of the Sunstone.docx` to Markdown and move chapter files into `manuscripts/book1/` (one MD file per chapter). I can do this conversion and split for you.
2. Split `updated_project_package.md` into the `world/` and `style/` files above. This makes the reference library easier to maintain and reference from your manuscript.
3. Add a `.gitignore` (ignore `dist/`, `*.docx` if you don't want binaries tracked) and a simple `LICENSE` file (CC-BY for lore, MIT for tools is common).
4. Create `scripts/generate_report.sh` to build PDFs from Markdown using Pandoc + XeLaTeX. Add a GitHub Actions workflow to automatically build PDFs on push and upload them as artifacts.
5. Add small validation tools:
	 - a link-checker for cross-references
	 - a spell-check workflow (GitHub Action using vale or codespell)

## Short-term tooling suggestion (minimal)
Install in your dev environment:

```bash
sudo apt update
sudo apt install -y pandoc texlive-xetex
```

Example script (place in `scripts/generate_report.sh` and make executable):

```bash
#!/usr/bin/env bash
set -euo pipefail
INPUT="$1"
OUTDIR="dist"
mkdir -p "$OUTDIR"
BASENAME="$(basename "$INPUT" .md)"
pandoc "$INPUT" --from markdown+yaml_metadata_block --pdf-engine=xelatex --toc -V geometry:margin=1in -o "$OUTDIR/${BASENAME}.pdf"
echo "Built $OUTDIR/${BASENAME}.pdf"
```

## How to keep track of changes and maintain consistency
- Use one file per character: `world/characters/anya.md` with voice taglines and allowed imagery. Use this file while editing dialogue.
- Keep canonical names and dates in `world/timeline.md`. When you update a timeline event, reference the chapter where it changed.
- Use YAML front-matter in chapter Markdown files to capture metadata (title, chapter number, POV character, date in-world).
- Commit often with descriptive messages: "Refactor: split updated_project_package into world/magic.md".
- Use branches per feature (e.g., `feat/character-anya-voice`) and PRs to review major changes.

## Low-risk automations I can add
- Convert `.docx` to Markdown and split into chapters
- Split `updated_project_package.md` into a `world/` folder with focused files
- Add `.gitignore`, `LICENSE`, and `scripts/generate_report.sh`
- Add a GitHub Action that builds PDFs and uploads artifacts on push

## Would you like me to:
1. Convert the Word manuscript to Markdown and split into `manuscripts/book1/`? (recommended)
2. Split `updated_project_package.md` into `world/` and `style/` files automatically? (recommended)
3. Add the build script and a GitHub Actions workflow to build PDFs on push?

Tell me which items to do and I'll implement them now. If you want to keep `.docx` as primary, say so and I'll only add reference files and the README.

---
Generated on: 2025-10-17
