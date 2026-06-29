# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A documentation site built with [MkDocs](https://www.mkdocs.org/) and the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme. The actual content is the prose in `docs/*.md` — there is no application code. (`main.py` is leftover scaffolding from `uv init` and is unused.)

## Writing style & voice

The content matters more than the tooling — this is a curated knowledge guide about AI coding / Claude Code, written to be shared. Keep every page consistent with these rules:

- **Language: English prose.** All explanatory text is in English.
- **Voice:** Use **"I"** for personal experience and opinions ("this workflow worked well for *me*"). Use **"we"** for step-by-step instructions and walking the reader through something ("*we'll* use Claude Code to..."). Keep it conversational, not formal.
- **Audience = future me, who is a non-expert.** Don't assume prior context; explain enough that someone new to AI coding can follow. But keep it light — this is a personal notes guide, not a textbook.
- **Plain and short.** Prefer bullet points and numbered steps over long paragraphs. Note only "the good stuff."
- **Curated, not exhaustive — this is NOT a wiki.** Do not try to document everything. For full detail, link out to official docs or other sources (e.g. the Claude quickstart, support articles) rather than reproducing them.

## Page conventions

- Each page starts with a single `#` H1 matching its topic; use `##` for sections (so the in-page table of contents works).
- Navigation order and titles are set explicitly in the `nav:` block of `mkdocs.yml` — when adding a page, add it there in the intended reading order (don't rely on alphabetical auto-nav).
- Images live in `docs/images/` and are referenced with **forward slashes**: `![alt](images/foo.png)`. Backslashes break rendering on the built site.

## Commands

Dependencies are managed with [uv](https://docs.astral.sh/uv/) (see `uv.lock`, `.python-version` pins 3.11).

```bash
uv sync                  # install dependencies into .venv
uv run mkdocs serve      # live-reload preview at http://127.0.0.1:8000
uv run mkdocs build      # build static site into ./site
uv run mkdocs gh-deploy  # build and push to the gh-pages branch
```

## Architecture & conventions

- **`mkdocs.yml`** is the site config. Note it has **no `nav:` key**, so MkDocs auto-generates navigation from the files in `docs/`. Adding a `.md` file under `docs/` makes it appear in the nav automatically; ordering/titles follow MkDocs defaults unless a `nav:` block is added.
- **Theming: deep steel-navy primary + aged-brass accent.** The palette is set to `custom` for both light (`default`) and dark (`slate`) schemes in `mkdocs.yml`, and the actual color values live in `docs/stylesheets/extra.css` (CSS variables like `--navy-steel` and `--brass`). Prose links are underlined and use the brass accent. To change colors, edit that CSS file rather than `mkdocs.yml`.
- **Images** go in `docs/images/` and are referenced from the Markdown pages.

## Deployment

`.github/workflows/ci.yml` runs on push to `main` or `master`: it `pip install mkdocs-material` and runs `mkdocs gh-deploy --force`, publishing to the `gh-pages` branch. Note CI installs mkdocs-material directly via pip rather than from `uv.lock`, so keep the dependency set in `pyproject.toml`/`uv.lock` aligned with what the site actually needs.
