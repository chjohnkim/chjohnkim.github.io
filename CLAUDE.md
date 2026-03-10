# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a static personal academic website for John Kim (Chung Hee Kim), a PhD candidate at CMU Robotics Institute. It is deployed via GitHub Pages at chjohnkim.github.io. There is no build system, package manager, or framework — all files are plain HTML, CSS, and JavaScript.

## Local Development

To preview the site locally, serve the root directory with any static file server:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

Opening `index.html` directly as a `file://` URL also works for most features.

## Architecture

- **`index.html` + `stylesheet.css`** — the current site with a modern card-based layout, CSS custom properties, and a built-in dark/light mode toggle.
- **`projects/projects.html`** — projects page, uses the same `stylesheet.css` and theme system as `index.html`.
- **`arxiv/index.html`** — legacy version, do not update.

### Theme System (main site)

The main site uses CSS variables defined on `:root` for light mode and overridden under `[data-theme="dark"]` in `stylesheet.css`. The `<html>` element's `data-theme` attribute is set by inline script on page load (defaults to `light`) and toggled by the `toggleTheme()` JS function, which also persists the choice to `localStorage`.

### Content Structure

Each research paper in `index.html` follows this `.paper-card` pattern:
```html
<div class="paper-card">
  <div class="paper-media">
    <video playsinline muted autoplay loop>
      <source src="images/VIDEO.mp4" type="video/mp4">
    </video>
  </div>
  <div class="paper-info">
    <a href="PAPER_URL"><span class="paper-title">TITLE</span></a>
    <span class="authors">...</span>
    <span class="venue"><em>VENUE YEAR</em></span>
    <div class="paper-links"><a href="">[Link]</a></div>
    <p class="paper-desc">DESCRIPTION</p>
  </div>
</div>
```

Award links use the `.award` CSS class (styled red in both light and dark modes).

### Key Asset Locations

- `images/` — demo videos (.mp4, .mov) for each paper
- `data/` — PDFs (CV, conference posters)
- `logos/` — institution/company logos (referenced from both `index.html` and `arxiv/index.html`)
- `projects/` — standalone project subpages (`projects.html` uses the revamped stylesheet; `l3dv/` is a legacy subpage, do not update)
