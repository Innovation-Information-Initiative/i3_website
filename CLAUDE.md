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

The site uses **automatic content discovery** with folder-based organization:

- **Events** and **News** use folder structures with individual `index.qmd` files
- **Quarto listing feature** automatically discovers and displays content
- **Featured filtering** controls which items appear on the homepage using `featured: true` in YAML front matter
- **Publications** still use `publications.yml` for centralized management

All template content from Deep Policy Lab has been removed - the site is clean and ready for I³ content migration.

### Key Configuration Files

- `_quarto.yml`: Main site configuration including navbar, theme, search, and global settings
- `index.qmd`: Homepage with custom layout using Quarto listing blocks for news/events/publications
- `references.bib`: Bibliography file for academic citations

### Content Types

**News**: Folder-based structure with automatic discovery
- Location: `news/item-name/index.qmd`
- Required front matter: title, subtitle, description, author, date, image, categories
- Images stored in: `news/item-name/images/`
- Set `featured: true` to display on homepage
- All news items automatically appear on `news.qmd`

**Events**: Folder-based structure with automatic discovery
- Location: `events/event-name/index.qmd`
- Required front matter: title, subtitle, description, author, date, image, categories
- Images stored in: `events/event-name/images/`
- Set `featured: true` to display on homepage
- All events automatically appear on `events.qmd`

**Publications**: Add entries to `publications.yml`
- Fields: path, image, title, subtitle, description, date, fulltext, categories
- Displayed on `publications.qmd` and homepage
- Can filter by categories (e.g., "featured")

**Essays**: Create individual `.qmd` files
- Page: `essays.qmd`

**Datasets**: Edit `datasets.qmd` directly with dataset information

### Listing System

The site uses Quarto's listing feature with automatic discovery and filtering:

**Homepage (`index.qmd`):**
- `#news-events` listing: Auto-discovers from `events/*/index.qmd` and `news/*/index.qmd`
  - Uses `include: featured: true` to filter homepage items
  - Shows only content marked as `featured: true` in front matter
- `#publications` listing: Pulls from `publications.yml`

**Individual listing pages:**
- `events.qmd`: Auto-discovers all events from `events/*/index.qmd`
- `news.qmd`: Auto-discovers all news from `news/*/index.qmd`

**Listing features:**
- Automatic content discovery using glob patterns
- Sorting (e.g., "date desc")
- Multiple content sources
- Grid/table layouts
- Filtering by YAML front matter fields using `include`/`exclude`
- Custom field display

### Styling and Theming

- `styles.css`: Main site stylesheet
- `custom.css`: Additional custom styles (used on homepage)
- `center.css`: Specific layout styles
- Theme set to "cosmo" in `_quarto.yml`
- Navbar colors: background `#05336B`, foreground `#FFFFFF`

### Static Assets

- `events/*/images/`: Event-specific images (stored with each event)
- `news/*/images/`: News-specific images (stored with each news item)
- `/files/images/`: Legacy image storage for publications, people, shared assets
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
1. Create folder: `news/news-item-name/`
2. Create `news/news-item-name/index.qmd` with front matter:
   ```yaml
   ---
   title: "News Item Title"
   subtitle: "Brief subtitle"
   description: "Longer description for listings"
   author: "Author Name"
   date: "YYYY-MM-DD"
   image: images/image-name.png
   categories: [category1, category2]
   featured: true  # Set to true to show on homepage
   ---
   ```
3. Add images to `news/news-item-name/images/`
4. Write content below front matter
5. Preview with `quarto preview`

**Add an event:**
1. Create folder: `events/event-name/`
2. Create `events/event-name/index.qmd` with front matter:
   ```yaml
   ---
   title: "Event Title"
   subtitle: "Event subtitle"
   description: "Event description for listings"
   author:
     - Author One
     - Author Two
   date: "YYYY-MM-DD"
   image: images/image-name.png
   categories: [workshop, category2]
   featured: true  # Set to true to show on homepage
   ---
   ```
3. Add images to `events/event-name/images/`
4. Write event details below front matter
5. Preview changes

**Add a publication:**
1. Open `publications.yml`
2. Add entry with path, image, title, subtitle, description, date, fulltext, categories
3. Use categories for filtering (e.g., "featured")
4. Preview changes

**Controlling homepage display:**
- Set `featured: true` in the front matter to show an event or news item on the homepage
- Set `featured: false` or omit the field to hide from homepage
- All items appear on their respective listing pages (`events.qmd` or `news.qmd`) regardless of featured status

## Deployment

The site uses a two-stage deployment process:

1. **GitHub Actions** (`/.github/workflows/quarto-build.yml`) builds the site on every commit to `main`:
   - Runs `quarto render` automatically
   - Publishes built site to `deploy` branch
   - Uses `peaceiris/actions-gh-pages` action

2. **Netlify** serves the pre-built site from the `deploy` branch:
   - No build step on Netlify (configured in `netlify.toml`)
   - Simply serves static files from the branch
   - Live site: **www.i3open.org**

Simply commit and push changes to `main` to trigger the build and deployment. No need to manually run `quarto render`.
