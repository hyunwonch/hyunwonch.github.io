# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

Academic portfolio website for Hyunwon Chung (PhD student, University of Michigan) built on the **al-folio** Jekyll theme. Hosted on GitHub Pages at hyunwonch.github.io.

## Build & Serve Commands

**Docker (recommended):**
```bash
docker compose up
# Site at http://localhost:8080, livereload on port 35729
```

**Local Ruby:**
```bash
bundle install
bundle exec jekyll serve --lsi
# Site at http://localhost:4000
```

**Production build (matches CI):**
```bash
export JEKYLL_ENV=production
bundle exec jekyll build --lsi
purgecss -c purgecss.config.js
```

## CI/CD

GitHub Actions (`.github/workflows/deploy.yml`) deploys on push to main/master:
- Ruby 3.2.2, installs jupyter + mermaid.cli + purgecss
- Builds with `jekyll build --lsi` in production mode
- Purges unused CSS, deploys `_site/` to gh-pages branch

## Architecture

**Jekyll layout chain:** Pages use front matter to select a layout from `_layouts/` (e.g., `about.html`, `post.html`, `page.html`). Layouts compose partials from `_includes/`. The base is `default.html`.

**Key directories:**
- `_pages/` — Main site pages (about, blog, chips, cv, projects). The about page is the homepage.
- `_posts/` — Blog posts (Markdown with front matter for tags/categories)
- `_bibliography/papers.bib` — Publications managed via jekyll-scholar (APA style, grouped by year descending)
- `_data/` — Structured data: `cv.yml`, `coauthors.yml`, `repositories.yml`, `venues.yml`
- `_sass/` — SCSS partials; `_base.scss` has component styles including chip gallery, `_themes.scss` defines light/dark CSS variables, `_variables.scss` has color palette
- `_plugins/` — Custom Ruby plugins (cache-bust, details tag, external-posts, file-exists, BibTeX keyword filter)
- `assets/json/resume.json` — JSON Resume format data, loaded via jekyll-get-json

**CSS framework:** Bootstrap 4 (MDB 4.20.0) with SCSS. Entry point is `assets/css/main.scss`. Light/dark mode theming uses CSS custom properties toggled at runtime.

**Collections:** `news` and `projects` are Jekyll collections defined in `_config.yml`.

## Conventions

- Blog categories: `technical`, `code`, `thoughts`
- Blog tags: `computer architecture`, `dataflow`, `VLSI`, `circuit`, `AI`
- Scholar config highlights papers by author last name `Chung`, first name `Hyunwon`
- External links open in new tab with `rel="external nofollow noopener"`
- ImageMagick generates responsive WebP images at 480/800/1400px widths from `assets/img/`
- The chips gallery page (`_pages/chips.md`) uses CSS Grid with flexbox card layout (styles in `_sass/_base.scss`)
