# Migration Guide: PubPub to Quarto

This guide helps you migrate content from the PubPub site (https://iii.pubpub.org/) to this Quarto website.

## Current Site Structure

The site has been cleaned and modernized with the following structure:

1. **Navigation Pages**:
   - About (`about.qmd`)
   - I3 Essays (`essays.qmd`)
   - News (`news.qmd`)
   - Events (`events.qmd`)
   - Publications (`publications.qmd`)
   - Public Datasets (`datasets.qmd`)
   - Contact (`contact.qmd`)

2. **Homepage** (`index.qmd`):
   - Features recent news, events, and publications
   - Custom layout with I³ branding
   - Pulls from YAML data files

3. **Content is Ready for Migration**:
   - All template content has been removed
   - YAML files are clean with example structures
   - Pages are configured and ready for content

## Content Migration Steps

### 1. News Items

Add news entries to `news.yml`:

```yaml
- path: https://example.com/article
  image: /files/images/news/example.jpg
  title: "I³ Announces New Dataset Release"
  subtitle: "Innovation Information Initiative"
  description: "Brief description of the news item"
  date: "2024-01-15"
```

### 2. Events

Add events to `events.yml`:

```yaml
- path: /events/2024-technical-working-group/
  image: /files/images/events/twg-2024.jpg
  title: "2024 Technical Working Group Meeting"
  author: "I³ Team"
  description: "Annual meeting of the Innovation Information Initiative technical working group"
  date: "2024-12-06"
  categories: [workshop]
```

### 3. Publications

Add publications to `publications.yml`:

```yaml
- path: https://doi.org/10.1234/example
  image: /files/images/journal/nature.jpg
  title: "Innovation Metrics and Patent Data"
  subtitle: "*Nature*"
  description: "Analysis of innovation metrics using patent citation data"
  date: "2024-01-01"
  fulltext: "[pdf](https://example.com/paper.pdf)"
  categories: [featured, patents]
```

### 4. Essays

Create individual essay files or add to an `essays.yml` file:

- Place essay `.qmd` files in an `essays/` directory
- Or create `essays.yml` following the same structure as news/events
- Update `essays.qmd` to list them using Quarto's listing feature

### 5. Datasets

Update `datasets.qmd` directly with:

- Dataset descriptions
- Links to datasets
- GitHub repositories
- Data portals

### 6. Images

Store images in `/files/images/`:

```
/files/images/
├── news/          # News item images
├── events/        # Event images
├── journal/       # Journal/publication logos
└── ...            # Other categories
```

Update image paths in YAML files to match: `/files/images/category/filename.jpg`

## Working with Quarto Listings

Quarto's listing feature automatically generates pages from YAML data:

### Basic Listing

In a `.qmd` file:

```yaml
---
listing:
- id: my-listing
  contents: mydata.yml
  sort: "date desc"
  type: grid
  fields: [image, title, subtitle, date]
---

:::{#my-listing}
:::
```

### Multiple Sources

Combine YAML files and directories:

```yaml
listing:
- id: combined
  contents:
    - data.yml
    - directory/
  sort: "date desc"
```

### Filtering

Show only specific categories:

```yaml
listing:
  contents: publications.yml
  include:
    categories: "featured"
```

## Workflow

### 1. Add Content

Edit YAML files or create new `.qmd` pages

### 2. Preview Locally

```bash
quarto preview
```

View changes at `http://localhost:XXXX`

### 3. Build for Production

```bash
quarto render
```

Generates static files in `docs/`

### 4. Deploy

Commit and push the `docs/` directory to GitHub for GitHub Pages deployment

## Tips

- **Consistency**: Use the same field names across similar content types
- **Images**: Always use absolute paths starting with `/files/images/`
- **Testing**: Preview locally before deploying
- **Incremental**: Migrate content in stages (news first, then events, etc.)
- **Validation**: Check that all image paths are correct after migration

## Resources

- [Quarto Documentation](https://quarto.org/docs/websites/)
- [Quarto Listings](https://quarto.org/docs/websites/website-listings.html)
- [YAML Syntax](https://yaml.org/spec/1.2.2/)

## Common Issues

**Images not showing**: Check that paths start with `/files/images/` and files exist

**Listing empty**: Ensure YAML file has valid syntax and proper indentation

**Build errors**: Run `quarto check` to diagnose issues

