# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Academic personal homepage for Tianshuo Peng (PhD student, MMLab@CUHK). Deployed as a static site via GitHub Pages at https://pengts.github.io/.

Design codename: **Lone-Trail** — a retro-scientific modernist style inspired by 20th-century space-age control panels, Swiss modernist typography, and scientific instrumentation aesthetics. No build step required; pure static HTML.

## Project Structure

```
pengts.github.io/
  .nojekyll              # Disables Jekyll on GitHub Pages
  index.html             # The live homepage (single self-contained HTML file)
  CLAUDE.md              # This file
  assets/
    img/
      my_pic_2025-10.JPG # Personal photo
    files/
      cv_pengts_251010.pdf # CV document
  _previews/             # Style exploration history (not served live)
```

## Development

No build tools. Open `index.html` in a browser to preview. All CSS is inline in `<style>`. Push to `main` branch to deploy.

## Design System

### Typography

- **Single font family**: `"Helvetica Neue", Helvetica, Arial, sans-serif`
- No monospace, no serif, no decorative fonts anywhere
- Hero name: 36-56px, weight 800, uppercase, tight letter-spacing (-.04em)
- Section titles: 16px, weight 700, uppercase, letter-spacing .1em, inside tab-style labels
- Body text: 15px, line-height 1.8
- Small text (labels, metadata): 10-13px

### Color System

Dark background with warm-toned content. Three accent colors with strict semantic meaning:

| Color | CSS Var | Hex | Usage |
|-------|---------|-----|-------|
| Carbon Black | `--ink` | #181818 | Page background base |
| Warm Paper | `--paper` | #F5EDDC | Primary text, headings |
| Lab Green (Teal) | `--teal` | #5C7F71 | Academic output: publication venues, code links, pub hover borders, paper news highlights |
| Low-Sat Green | `--teal-2` | #7A9E90 | News `.paper` bold text (readable on dark) |
| Archive Ochre | `--ochre` | #BA8530 | Personal identity: own name in author lists, external profile links (Scholar, GitHub, CV), InternAgent Team label |
| Signal Red | `--red` | #802520 | Honors & milestones: awards in news (bold text), award list bullet dots |
| Red-2 | `--red-2` | #A9473B | Award news bold text (brighter for readability) |

**Rules:**
- Green = academic output/papers
- Yellow/ochre = personal identity/self-reference
- Red = honors and milestones only
- Never use colors randomly; always follow semantic classification

### Background & Atmosphere Layers

The page builds depth through stacked layers (all via CSS, no images except noise SVG):

1. **Base gradient**: `radial-gradient` with teal tint top-left, red tint top-right, over ink-3 → ink vertical gradient
2. **CRT scanlines** (`body::before`): `repeating-linear-gradient` 1px white lines every 4px, mix-blend-mode screen, opacity .5
3. **Film grain** (`body::after`): Inline SVG `feTurbulence` noise texture, opacity .1
4. **Grid pattern** (hero): 80px grid lines at very low opacity (.04-.06)

### Key Design Elements

#### Navigation Bar (sticky)
- Left: Three small dots (5px circles, gap 4px) in teal/ochre/red + bold name
- Right: Section anchors (bold, uppercase) + separator line + external links (ochre, bold)
- Backdrop-filter blur, semi-transparent dark background

#### Hero Section
- Name with `text-shadow`: red offset right (3px, .55 opacity) + green offset left-down (-2px 2px, .4 opacity) — creates retro print misregistration effect
- Bio text in natural paragraphs, links with bottom-border underline
- Collaboration invitation paragraph prefixed by signal-tower SVG icon (three arcs in teal/ochre/red)
- Photo (240x300px) with subtle dual-gradient overlay and coordinate labels (top-left: lat/long, bottom-right: ID code)

#### Hero Decorative Elements (right side)
- NOT color stripes. Instead: orbital arcs (dashed/dotted circles rotating slowly), signal blip nodes (tiny glowing dots), vertical datastream ticks, scanline pattern
- Topology SVG (bottom-left): abstract node-link network diagram
- Radar sweep (center-right): concentric rings + rotating conic-gradient sweep

#### Section Titles (tab-style labels)
- Dark panel with subtle gradient background (`rgba(245,237,220,.06)` → `rgba(92,127,113,.04)`)
- Left edge: 5px wide tricolor bar (teal 33% / ochre 33% / red 33%, hard boundaries, no gradient)
- Right edge: faint light gradient sheen (`::after`)
- Text inside with padding

#### Research Interests
- Vertical list (not cards), grid: 200px title | 1fr description
- Colored left-border on hover: item 1 = teal, item 2 = ochre, item 3 = red
- Slide-right + background highlight on hover

#### News
- Grid: 90px date | content
- `.paper` class: bold text colored `--teal-2`
- `.award` class: bold text colored `--red-2`
- Dates all same color (no color differentiation on dates)
- Hover: slide-right with ochre gradient background
- Decorative: timeline-axis line on far left (teal→ochre→red gradient, with endpoint circles)

#### Publications
- Grid: 100px venue | body | links
- Venue label in teal, 13px bold
- Author's own name (and InternAgent Team) highlighted in ochre via `.me` class
- Hover: slide-right (4px), teal left-border appears, border brightens
- PDF/Code link buttons: bordered, uppercase, ochre on hover
- Decorative: concentric rings (right side, low opacity, middle ring rotates)

#### Awards
- Two-column grid of bordered items
- Red dot bullet (4px) before each item
- Hover: subtle red background tint

#### Invited Talks
- List with rotated diamond (45deg square, teal border) as bullet
- Links in ochre with underline

#### Section Dividers (between sections)
- Measurement ruler: horizontal line with tick marks (repeating gradient)
- Three colored node dots at 20%/50%/80% positions

#### Footer
- Mission stamp: bordered box with tricolor top-bar, uppercase small text
- Colophon line below

### Animation

- `fadeIn`: translateY(16px) + opacity on page load, staggered per section
- `slowSpin`: for orbital decorative rings (80-90s per revolution)
- `radarSpin`: 6s rotation for radar sweep element
- All hover transitions: 0.2-0.3s ease

### Responsive (max-width: 900px)

- Hero grid collapses to single column
- Photo centers and shrinks (180x220)
- Publication links hidden
- Awards grid becomes single column
- All decorative elements (topology, rings, radar, rulers, timeline, telemetry) hidden
- Nav links reduce gap, separator and mobile-hidden items disappear

## Content Editing Guide

### Adding a Publication

Insert a new `.pub-entry` div in the `pub-list`:

```html
<div class="pub-entry">
  <div class="pub-venue">VENUE YEAR</div>
  <div class="pub-body">
    <div class="title">Paper Title</div>
    <div class="authors">Author1, <span class="me">Tianshuo Peng</span>, Author3</div>
    <div class="conference">Full conference name, year</div>
  </div>
  <div class="pub-links">
    <a href="URL" class="pub-link">PDF</a>
    <a href="URL" class="pub-link">Code</a>
  </div>
</div>
```

Use `<span class="me">` for own name or team name (renders in ochre).

### Adding a News Item

```html
<li class="news-item paper">  <!-- or class="news-item award" -->
  <span class="date">Mon. YEAR</span>
  <span class="content">Text with <strong>highlighted part</strong>.</span>
</li>
```

- Use `.paper` for publication/research news (bold text turns green)
- Use `.award` for honors/awards (bold text turns red)

### Adding an Award

Add `<li>` inside `.awards-list`.

### Adding a Talk

Add `<li>` inside `.talks-list` with `<strong>` for title and `<a>` for institution links.

### Updating Photo

Replace `./assets/img/my_pic_2025-10.JPG` and update the `src` in hero-photo.

### Updating CV

Replace PDF in `assets/files/` and update the href in nav link.

## Design Principles

1. **No content invention**: Never add descriptive text, subtitles, or lead paragraphs that don't exist in the source content
2. **Semantic color only**: Every use of teal/ochre/red must follow the defined meaning
3. **Minimal page**: No unnecessary sections, decorations should be subtle atmosphere, not attention-grabbing
4. **Retro-scientific, not sci-fi**: Inspired by real control panels and instrumentation, not Hollywood sci-fi. Avoid glowing neon, sharp gradients, or flashy effects
5. **Single file simplicity**: Everything in one HTML file. No build steps, no dependencies, no frameworks
