---
title: Getting started
description: Learn how to start building your documentation website with Statidocs, powered by Cecil.
---
# Getting started

Statidocs is a documentation starter, built with the static site generator [Cecil](https://cecil.app) and its [_Docs_ theme](https://github.com/Cecilapp/theme-docs).

:::important
PHP 8.3+ is required.
:::

## Create a new project

The easiest way to create a new Statidocs project is using [Composer](https://getcomposer.org):

```bash
composer create-project cecil/statidocs --ask
```

:::info
This command also downloads the `cecil.phar` binary in your project directory.
:::

## Start the local server

When working locally, [Cecil’s built-in server](https://cecil.app/documentation/commands/#serve) lets you preview your work and automatically refreshes your browser when you make changes.

Inside your project directory, run the following command to start the local server:

```bash
php cecil.phar serve
```

This will log a message to your terminal with the URL of your local preview. Open this URL (<http://localhost:8000> by default) to start browsing your documentation.

## Add pages

### File formats

Statidocs supports authoring content in Markdown with no configuration required. You can extend default capabilities by enabling [Cecil’s Markdown options](https://cecil.app/documentation/content/#markdown).

### Organize pages

Add new pages to your site by creating `.md` files in `pages/docs/`. Use sub-folders to group pages: each sub-folder containing an `index.md` file becomes a collapsible group in the sidebar, at any depth.

For example, the following file structure will generate pages at `/docs/getting-started/`, `/docs/guides/i18n/` and `/docs/guides/advanced/customization/`:

```text
<my-project>
└─ pages
   └─ docs
      ├─ 1-Getting started.md
      └─ guides
         ├─ index.md
         ├─ 2-i18n.md
         └─ advanced
            ├─ index.md
            └─ 1-customization.md
```

Pages are sorted by `weight`: use a number prefix in the file name (e.g. `1-`), or the `weight` front matter variable.

:::tip
To learn more about the sidebar, read the [Navigation guide](page:docs/guides/navigation).
:::

### Front matter

All pages use front matter variables to control how the page appears:

```yaml
---
title: Hello world
description: This is a page description.
---
```

See the [front matter reference](page:docs/reference/front-matter) for the full list of variables.

## Build and deploy

When you are ready to publish, generate the static site in the `_site/` directory:

```bash
php cecil.phar build
```

Then upload the content of `_site/` to any static web host (Netlify, Vercel, GitHub Pages, etc.). See the [Cecil deployment documentation](https://cecil.app/documentation/deploy/) for more details.

## Update Statidocs

Statidocs is built on top of the Cecil theme _[Docs](https://github.com/Cecilapp/theme-docs)_. You can update it and other Cecil themes by running the following command in your terminal:

```bash
composer update
```

Update Cecil itself with its `self-update` command:

```bash
php cecil.phar self-update
```
