# Usage

This page covers the detailed usage of the Document Hosting project.

## Adding New Pages

To add a new documentation page:

1. Create a new Markdown file in the `docs/` directory
2. Add the page to the navigation in `mkdocs.yml`

## Configuration

The MkDocs configuration is stored in `mkdocs.yml`. You can customize:

- Site name and description
- Navigation structure
- Theme settings
- Markdown extensions

## Deploying to GitHub Pages

To deploy the documentation to GitHub Pages, run:

```bash
mkdocs gh-deploy
```

This will build the documentation and push it to the `gh-pages` branch.

## Customizing the Theme

The project uses the Material theme. You can customize the theme by modifying the `theme` section in `mkdocs.yml`:

```yaml
theme:
  name: material
  palette:
    primary: indigo
    accent: indigo
```

See the [Material for MkDocs documentation](https://squidfunk.github.io/mkdocs-material/) for more customization options.
