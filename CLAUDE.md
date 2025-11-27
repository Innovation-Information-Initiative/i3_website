# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the Innovation Information Initiative (I³) website, built with Quarto and migrated from PubPub. It's a static website for a data collaborative focused on open innovation data, patent datasets, citation graphs, and related analytics tools.

## Development Commands

### Preview the website locally
```bash
quarto preview
```
This starts a local development server with live reload. The site will be available at http://localhost:XXXX (port will be shown in output).

### Build the website
```bash
quarto render
```
This generates static files in the `_site/` directory, which is the output directory for deployment.

### Check Quarto version
```bash
quarto --version
```

## Architecture and Structure

### Content Organization

The site uses **YAML-based content management** for structured data:

- **YAML files** store metadata for news, events, publications, etc.
- **Quarto listing feature** automatically generates pages from YAML data
- **Individual pages** can supplement YAML content when needed

All template content from Deep Policy Lab has been removed - the site is clean and ready for I³ content migration.

### Key Configuration Files

- `_quarto.yml`: Main site configuration including navbar, theme, search, and global settings
- `index.qmd`: Homepage with custom layout using Quarto listing blocks for news/events/publications
- `references.bib`: Bibliography file for academic citations

### Content Types

**News**: Add entries to `news.yml`
- Fields: path, image, title, subtitle, description, date
- Displayed on `news.qmd` and homepage

**Events**: Add entries to `events.yml`
- Fields: path, image, title, author, description, date, categories
- Displayed on `events.qmd` and homepage

**Publications**: Add entries to `publications.yml`
- Fields: path, image, title, subtitle, description, date, fulltext, categories
- Displayed on `publications.qmd` and homepage
- Can filter by categories (e.g., "featured")

**Essays**: Create individual `.qmd` files or use `essays.yml`
- Page: `essays.qmd`

**Datasets**: Edit `datasets.qmd` directly with dataset information

### Listing System

The homepage (`index.qmd`) demonstrates Quarto's listing feature:
- `#news-events` listing: Pulls from `events.yml` and `news.yml`
- `#publications` listing: Pulls from `publications.yml`
- Listings support:
  - Sorting (e.g., "date desc")
  - Multiple content sources
  - Grid/table layouts
  - Filtering by categories
  - Custom field display

### Styling and Theming

- `styles.css`: Main site stylesheet
- `custom.css`: Additional custom styles (used on homepage)
- `center.css`: Specific layout styles
- Theme set to "cosmo" in `_quarto.yml`
- Navbar colors: background `#05336B`, foreground `#FFFFFF`

### Static Assets

- `/files/images/`: Image storage for news, events, publications, people
- `/files/includes/`: Reusable content snippets (analytics, social sharing)
  - `_msclarity.qmd`: Microsoft Clarity analytics
  - `_mswebmaster.js`: Webmaster verification
  - `_academic.qmd`, `_socialshare.qmd`: Template includes

### Page Layouts

- **Standard pages**: Use `page-layout: full` (About, News, Events, Publications, etc.)
- **Homepage**: Uses `page-layout: custom` with Quarto's grid system
  - Grid classes: `.g-col-12`, `.g-col-md-7`, etc.
  - Background frames: `.background-frame`, `.alt-background`
  - Content blocks: `.content-block`

### Navigation

The site has a clean navigation structure in `_quarto.yml`:
- About
- I3 Essays
- News
- Events
- Publications
- Public Datasets
- Contact

All placeholder/template pages have been removed.

## Adding Content

### Quick Reference

**Add a news item:**
1. Open `news.yml`
2. Add entry with path, image, title, subtitle, description, date
3. Preview with `quarto preview`

**Add an event:**
1. Open `events.yml`
2. Add entry following the structure in the file comments
3. Preview changes

**Add a publication:**
1. Open `publications.yml`
2. Add entry with DOI/URL, journal, description, date
3. Use categories for filtering (e.g., "featured")

See `MIGRATION_GUIDE.md` for detailed migration instructions from PubPub.

## Deployment

The site is configured to output to the `docs/` directory for GitHub Pages deployment. After running `quarto render`, commit and push the `docs/` directory to deploy.
