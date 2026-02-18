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
- `_pages/` — Main site pages (about, blog, chips, cv). The about page is the homepage. Projects page exists but is hidden from nav.
- `_posts/` — Blog posts (Markdown with front matter for tags/categories). Filenames follow `YYYY-MM-DD-slug.md`.
- `_news/` — News announcements displayed on the about page. Use `inline: true` in front matter for inline content.
- `_bibliography/papers.bib` — Publications managed via jekyll-scholar (APA style, grouped by year descending)
- `_data/` — Structured data: `cv.yml`, `coauthors.yml`, `repositories.yml`, `venues.yml`
- `_sass/` — SCSS partials; `_base.scss` has component styles including chip gallery, `_layout.scss` has body/heading fonts, `_themes.scss` defines light/dark CSS variables, `_variables.scss` has color palette
- `_plugins/` — Custom Ruby plugins (cache-bust, details tag, external-posts, file-exists, BibTeX keyword filter)
- `assets/json/resume.json` — JSON Resume format data, loaded via jekyll-get-json

**CSS framework:** Bootstrap 4 (MDB 4.20.0) with SCSS. Entry point is `assets/css/main.scss`. Light/dark mode theming uses CSS custom properties toggled at runtime.

**Collections:** `news` and `projects` are Jekyll collections defined in `_config.yml`.

## Navbar

Order is controlled by `nav_order` in each page's front matter. Current order: about (homepage, no nav_order), chips (1), blog (2), cv (5). Projects is disabled (`nav: false`).

## Fonts

- **Body text:** `Source Serif 4` (serif) — loaded via Google Fonts in `_includes/head.html`
- **Headings/UI:** `Work Sans` (sans-serif)
- Bootstrap/MDB vendor CSS defaults to Roboto, so font overrides in `_sass/_layout.scss` use `!important` to take precedence. Common elements use `font-family: inherit !important` to follow the body font.

## CSS Specificity Gotchas

- Bootstrap/MDB set `font-family: Roboto` on many elements directly. Any font changes must use `!important` in `_layout.scss` to override.
- The global `.caption` class in `_base.scss` (line ~127) adds `margin-bottom: 1.5rem`. Component-specific `.caption` styles (e.g., in `.chip-card`) must use `!important` on margin/padding to override.

## Blog Posts

- Front matter: `layout: post`, `title`, `date`, `description`, `tags`, `categories`, `related_posts`
- Categories: `technical`, `code`, `thoughts`
- Tags: `computer architecture`, `dataflow`, `VLSI`, `circuit`, `AI`
- Liquid template engine processes all Markdown files — pipe characters `|` in content must be escaped as `&#124;`
- Always leave a blank line after blockquotes (`>`) or the next paragraph gets merged into the quote

## Chips Gallery

- Page: `_pages/chips.md` with CSS Grid layout (3 columns)
- Styles in `_sass/_base.scss` under `.chip-gallery`
- Captions use fixed `min-height` with flexbox centering to ensure equal height across cards
- Images are included via `{% include figure.html %}`

## Conventions

- Scholar config highlights papers by author last name `Chung`, first name `Hyunwon`
- External links open in new tab with `rel="external nofollow noopener"`
- ImageMagick generates responsive WebP images at 480/800/1400px widths from `assets/img/`
- News dates display as month and year only (format: `%b %Y`)
