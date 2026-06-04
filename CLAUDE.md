# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Academic personal homepage for Tianshuo Peng. Deployed via GitHub Pages at https://pengts.github.io/.

The site is transitioning from Jekyll (Minimal Light theme) to a new standalone design codenamed **Lone-Trail** — a retro-scientific modernist style. The reference implementation is at `_previews/style_5_lone_trail.html`.

## Development Commands

```bash
# Install dependencies (Jekyll, legacy build)
bundle install

# Run local development server (view at http://localhost:4000)
bundle exec jekyll serve

# Build static site (output to _site/)
bundle exec jekyll build
```

## Architecture (Legacy Jekyll)

- `_config.yml` — Site configuration: personal info, links, SEO, theme options
- `index.md` — Main page content (Markdown + HTML, uses `layout: homepage`)
- `_data/publications.yml` — Publication list in YAML format
- `_includes/publications.md` — Publication rendering template
- `_layouts/homepage.html` — HTML layout template
- `_sass/minimal-light.scss` — Main stylesheet
- `assets/` — Static files: images (`img/`), PDFs (`files/`), CSS, JS

## Design System: Lone-Trail

Reference file: `_previews/style_5_lone_trail.html`

### Visual Identity

- **Font**: Helvetica Neue / Helvetica (single font family throughout)
- **Background**: Dark (carbon black #181818) with radial gradient atmosphere, CRT scanline overlay, film grain noise texture
- **Layout**: Swiss modernist grid, 1080px max-width

### Color Palette & Semantic Rules

Three accent colors used with clear meaning:

| Color | Var | Hex | Semantic |
|-------|-----|-----|----------|
| Teal (Lab Green) | `--teal` | #5C7F71 | Academic output: paper venues, code links, pub hover borders |
| Ochre (Archive Yellow) | `--ochre` | #BA8530 | Personal identity: author name highlight, external profile links (Scholar, GitHub, CV) |
| Red (Signal) | `--red` | #802520 | Honors & milestones: awards, scholarships, academic honors in news |

### Key Design Elements

- **Nav mark**: Three vertical color bars (teal/ochre/red) side-by-side, no gap, top-bottom fade to transparent
- **Hero stripes**: Background decorative vertical bands (same 3 colors), right-aligned, mix-blend-mode screen
- **Section titles**: Uppercase, preceded by a short tricolor gradient bar
- **Publications**: Grid layout (venue | title+authors | links), teal hover left-border
- **Research Interests**: Vertical list with left-aligned title + right-aligned description, colored left-border on hover (teal/ochre/red for items 1/2/3)
- **News items**: Date + content grid; `.paper` class = green bold text; `.award` class = red date + red bold text

### Content Rules

- Do not add descriptive text that doesn't exist in the original content
- Keep the page minimal — no unnecessary subtitles or lead paragraphs
- External links (Scholar, GitHub, CV) belong in the top navigation, not the footer
- Photo placement: right side of hero section

## Content Editing

- **Bio/news/research interests**: Edit directly in the HTML
- **Publications**: Add entries following the existing `.pub-entry` structure
- **Photo**: Replace `./assets/img/my_pic_2025-10.JPG`
- **CV PDF**: Update path in nav link (currently `assets/files/cv_pengts_251010.pdf`)
