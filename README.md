# Artissist Website

This repository contains the Jekyll-based documentation website for the Artissist project - an Artist's Personal Assistant platform.

## Overview

The website is built with Jekyll and automatically deployed to GitHub Pages. All content is organized in the `_docs/` collection as markdown files, providing a consistent structure for documentation and pages.

## Repository Structure

```
├── _config.yml           # Jekyll configuration
├── Gemfile              # Ruby dependencies
├── _docs/               # All site content
│   ├── index.md         # Homepage
│   ├── about.md         # About page
│   ├── docs.md          # Documentation index
│   ├── architecture.md  # Architecture overview
│   └── data-model.md    # Data model documentation
└── .github/
    └── workflows/
        └── pages.yml     # GitHub Actions deployment
```

## Local Development

### Prerequisites

- Ruby 3.1 or higher
- Bundler gem

### Setup

1. Clone the repository:
```bash
git clone <repository-url>
cd website
```

2. Install dependencies:
```bash
bundle install
```

3. Start the development server:
```bash
bundle exec jekyll serve
```

4. Open your browser to `http://localhost:4000/website/`

### Development Commands

```bash
# Start development server with live reload
bundle exec jekyll serve

# Start server with drafts enabled
bundle exec jekyll serve --drafts

# Build the site (output to _site/)
bundle exec jekyll build

# Clean build artifacts
bundle exec jekyll clean
```

## Adding and Editing Pages

### Adding a New Page

1. Create a new markdown file in the `_docs/` directory:
```bash
touch _docs/new-page.md
```

2. Add front matter and content:
```markdown
---
layout: page
title: "Your Page Title"
---

# Your Page Title

Your content here...
```

3. The page will be automatically available at `/website/docs/new-page/`

### Editing Existing Pages

Simply edit the markdown files in `_docs/`. Changes will be reflected immediately in development mode or after the next deployment.

### Page Structure

All pages should include front matter:
```yaml
---
layout: page           # Use 'page' for all content
title: "Page Title"    # Appears in navigation and <title>
permalink: /custom/    # Optional: override default URL
published: true        # Optional: set to false to exclude from build
---
```

### Excluding Pages from Build

To exclude a page from the build process, use `published: false` in the front matter:

```yaml
---
layout: page
title: "Draft Page"
published: false       # This page won't appear in production
---

# This page is excluded from the build
```

**Alternative Methods:**

1. **Drafts Directory**: Move files to `_drafts/` folder (excluded by default)
2. **Config Exclusion**: Add specific files to `exclude:` list in `_config.yml`
3. **Development Only**: Use `--unpublished` flag to include unpublished pages locally:
   ```bash
   bundle exec jekyll serve --unpublished
   ```

### Navigation

Pages are automatically included in site navigation. To customize navigation, edit the `header_pages` section in `_config.yml`:

```yaml
header_pages:
  - _docs/about.md
  - _docs/docs.md
```

## Content Guidelines

### Writing Style
- Use clear, concise language
- Include code examples where relevant
- Add proper headings for navigation
- Link to related pages when appropriate

### Markdown Features
- Standard markdown syntax
- Code syntax highlighting with language tags
- Front matter for metadata
- Jekyll collections for organization

### Adding Code Examples
```markdown
```javascript
// JavaScript example
const example = "Hello World";
```
```

## GitHub Pages Deployment

### Automatic Deployment

The site automatically deploys to GitHub Pages when changes are pushed to the `main` branch via GitHub Actions.

**Deployment Process:**
1. Push changes to `main` branch
2. GitHub Actions workflow triggers
3. Jekyll builds the site
4. Site deploys to GitHub Pages
5. Available at: `https://artissist.github.io/website/`

### Manual Deployment

To trigger a manual deployment:
1. Go to the "Actions" tab in GitHub
2. Select "Deploy Jekyll with GitHub Pages dependencies preinstalled"
3. Click "Run workflow"

### Deployment Configuration

The deployment is configured in `.github/workflows/pages.yml` with:
- Ruby 3.1 setup
- Bundler caching for faster builds
- Jekyll build with GitHub Pages compatibility
- Automatic artifact upload and deployment

## Configuration

### Site Settings

Key configuration options in `_config.yml`:

```yaml
title: "Mosaic - Artist's Personal Assistant"
description: "A personal assistant platform designed to streamline creative workflows for artists"
baseurl: "/website"                    # GitHub Pages subpath
url: "https://artissist.github.io"     # GitHub Pages domain
```

### Jekyll Plugins

The site uses these Jekyll plugins:
- `jekyll-feed`: RSS feed generation
- `jekyll-sitemap`: XML sitemap
- `jekyll-seo-tag`: SEO meta tags

### Theme

Uses the default `minima` theme with customizations possible through:
- Custom CSS in `assets/css/style.scss`
- Layout overrides in `_layouts/`
- Include overrides in `_includes/`

## Troubleshooting

### Common Issues

**Build failures:**
- Check Jekyll version compatibility with GitHub Pages
- Ensure all front matter is properly formatted
- Validate YAML syntax in `_config.yml`

**Missing pages:**
- Verify file is in `_docs/` directory
- Check front matter includes `layout: page`
- Ensure permalink doesn't conflict with existing pages

**Local development issues:**
- Run `bundle install` to update dependencies
- Clear cache with `bundle exec jekyll clean`
- Check Ruby version compatibility

### Getting Help

1. Check the [Jekyll documentation](https://jekyllrb.com/docs/)
2. Review [GitHub Pages documentation](https://docs.github.com/en/pages)
3. Examine build logs in GitHub Actions for deployment issues

## Contributing

1. Create a new branch for your changes
2. Add or edit markdown files in `_docs/`
3. Test locally with `bundle exec jekyll serve`
4. Submit a pull request
5. Changes will automatically deploy once merged to `main`

## Links

- **Live Site**: https://artissist.github.io/website/
- **Main Project**: [Artissist Repository](https://github.com/artissist/mosaic)
- **Jekyll Documentation**: https://jekyllrb.com/docs/
- **GitHub Pages**: https://pages.github.com/