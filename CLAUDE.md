# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal academic website for Hyunwon Chung (PhD student, University of Michigan) built with Jekyll using the **al-folio** theme. Deployed to GitHub Pages at `https://hyunwonch.github.io`.

## Build & Development Commands

**Local development with Docker (recommended):**
```bash
docker compose up
```
Serves at `http://localhost:8080` with live reload on port 35729.

**Local development without Docker:**
```bash
bundle install
bundle exec jekyll serve --lsi
```
Serves at `http://localhost:4000`.

**Production build:**
```bash
JEKYLL_ENV=production bundle exec jekyll build --lsi
```

## Deployment

Automated via GitHub Actions (`.github/workflows/deploy.yml`). Pushing to `master` triggers a build and deploy to the `gh-pages` branch. The workflow installs Ruby 3.2.2, builds Jekyll with `--lsi`, runs PurgeCSS, then deploys.

## Architecture

This is a Jekyll site based on al-folio. Key directories:

- **`_config.yml`** — Central configuration: site metadata, plugin settings, scholar config, feature flags. Most site-wide changes start here.
- **`_pages/`** — Top-level pages (about, blog, cv, projects). These are Markdown files with YAML front matter.
- **`_layouts/`** — HTML layout templates (about, post, distill, cv, etc.). Pages reference these via `layout:` in front matter.
- **`_includes/`** — Reusable HTML partials (header, footer, CV components in `cv/`, resume components in `resume/`).
- **`_bibliography/papers.bib`** — BibTeX file for publications. Processed by `jekyll-scholar` plugin with APA style, grouped by year descending. Author highlight is configured for "Chung, Hyunwon".
- **`_data/`** — YAML data files: `cv.yml` (CV structure), `repositories.yml` (GitHub repos to display), `venues.yml`, `coauthors.yml`.
- **`assets/json/resume.json`** — JSON Resume data loaded at build time via `jekyll-get-json` plugin.
- **`_news/`** — Announcement items displayed on the about page.
- **`_posts/`** — Blog posts. Permalink pattern: `/blog/:year/:title/`.
- **`_plugins/`** — Custom Ruby plugins (cache busting, external posts, file existence checks).
- **`_sass/`** — Sass stylesheets for theming and layout customization.
- **`assets/`** — Static files (CSS, JS, images, fonts, PDFs).

## Key Configuration Details

- **Feature flags** in `_config.yml` control dark mode, math (MathJax), masonry layout, medium zoom, progress bar, and project categories — all toggled via `enable_*` booleans.
- **Collections**: `news` and `projects` are defined as Jekyll collections with their own output paths.
- **Responsive images**: ImageMagick generates WebP variants at 480/800/1400px widths. Requires `convert` on PATH.
- **Blog tags/categories**: `display_tags` and `display_categories` in `_config.yml` control what appears on the blog front page.
- **Scholar configuration**: `max_author_limit: 3`, publication badges (Altmetric, Dimensions), BibTeX filters for LaTeX/smallcaps/superscript.

## Content Editing Patterns

- **Adding a publication**: Add BibTeX entry to `_bibliography/papers.bib`. Use `preview:` key for thumbnails, `selected: true` for featured publications.
- **Adding a news item**: Create a new `.md` file in `_news/` with date in filename.
- **Adding a blog post**: Create a new `.md` file in `_posts/` following `YYYY-MM-DD-title.md` naming.
- **Updating CV**: Edit `_data/cv.yml` for the structured CV page, or `assets/json/resume.json` for the JSON Resume format.
