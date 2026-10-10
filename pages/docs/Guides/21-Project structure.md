---
title: Project structure
description: This guide will show you how a Statidocs project is organized and what the different files in your project do.
---
# Project structure

This guide will show you how a Statidocs project is organized and what the different files in your project do.

Statidocs projects follow the same file and directory structure as Cecil projects. See [Cecil’s files organization documentation](https://cecil.app/documentation/content/#files-organization) for more detail.

## Example

```text
<my-project>
├─ assets/
│  ├─ favicon.png
│  └─ logo.png
├─ data/
│  └─ authors.yml
├─ layouts/
├─ pages/
│  ├─ docs/
│  │  ├─ index.md
│  │  ├─ Introduction/
│  │  │  ├─ index.md
│  │  │  └─ 11-Getting started.md
│  │  └─ Guides/
│  │     ├─ index.md
│  │     └─ 21-Project structure.md
│  ├─ about.md
│  └─ index.md
├─ static/
├─ themes/
│  └─ docs/
├─ translations/
│  └─ messages.fr.yaml
├─ cecil.yml
└─ composer.json
```

## Files and directories

- `cecil.yml` — The [configuration](page:docs/reference/configuration) file.
- `composer.json` — Dependencies of the project: Cecil themes (_Docs_, _PWA_, etc.).
- `pages/` — The content of your site, written in Markdown:
  - `pages/index.md` — The homepage, built from [blocks](page:docs/guides/customization) defined in its front matter.
  - `pages/docs/` — Each Markdown file (`.md`) in this directory turns into a documentation page; each sub-directory with an `index.md` file turns into a [sidebar group](page:docs/guides/navigation).
- `assets/` — Assets (styles, images, favicon, PDFs, etc.) that will be processed (resized, optimized, fingerprinted, etc.).
- `static/` (optional) — Files copied as is in the generated site.
- `data/` (optional) — Data files (YAML, JSON, CSV, etc.) available in templates, like the authors list.
- `layouts/` (optional) — Your own [Twig](https://twig.symfony.com) templates, to override those of the theme.
- `themes/` — Installed themes, managed by Composer: do not edit them directly.
- `translations/` (optional) — Translation data to support [internationalization](page:docs/guides/internationalization).

:::info
The `_site/` directory (generated site) and the `.cache/` directory are created by Cecil: they don’t need to be versioned.
:::
