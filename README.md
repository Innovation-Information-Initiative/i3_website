# Innovation Information Initiative (i3) Website

[![Build Quarto](https://github.com/Innovation-Information-Initiative/i3_website/actions/workflows/quarto-build.yml/badge.svg)](https://github.com/Innovation-Information-Initiative/i3_website/actions/workflows/quarto-build.yml)

The official website for the Innovation Information Initiative, built with [Quarto](https://quarto.org/).

## Prerequisites

- [Quarto](https://quarto.org/) - Install by following the [official installation guide](https://quarto.org/docs/get-started/)

## Quick Start

### Preview Locally
```bash
quarto preview
```
This starts a local development server with live reload.

### Build the Website
```bash
quarto render
```
This generates static files in the `_site/` directory.

### Adding Content

Content uses automatic discovery with folder-based organization:

#### News Items
1. Create folder: `news/item-name/`
2. Create `news/item-name/index.qmd` with YAML front matter
3. Add images to `news/item-name/images/`
4. Set `featured: true` to display on homepage

#### Events
1. Create folder: `events/event-name/`
2. Create `events/event-name/index.qmd` with YAML front matter
3. Add images to `events/event-name/images/`
4. Set `featured: true` to display on homepage

#### Other Content Types
- **Publications**: Add entries to `publications.yml`
- **Datasets**: Update `datasets.qmd` with dataset information

See `CLAUDE.md` for detailed examples and YAML front matter templates.

## Deployment

The site uses a two-stage deployment process:

1. **GitHub Actions** builds the site on every commit to `main`
   - Runs `quarto render` automatically
   - Publishes built site to `deploy` branch
   - Build status shown in badge above

2. **GitHub Pages** serves the pre-built site from the `deploy` branch, with **Cloudflare** handling DNS routing
   - **Live site**: www.i3open.org

Simply commit and push changes to `main` to trigger the build and deployment.

## License

Licensed under GPL-3.0. Based on the [Deep Policy Lab website template](https://github.com/deeppolicylab/deeppolicylab.github.io).
