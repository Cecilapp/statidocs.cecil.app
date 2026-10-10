---
title: FAQ
description: Frequently asked questions about Statidocs.
---
# FAQ

## What is the difference between Statidocs and the Docs theme?

The [_Docs_ theme](https://github.com/Cecilapp/theme-docs) provides the templates and styles. Statidocs is a ready-to-use project (configuration, pages structure, translations, PWA) built on top of it: the fastest way to start a documentation website with [Cecil](https://cecil.app).

## Is Node.js required?

No. Cecil is a PHP application, and the CSS of the theme is compiled with the Tailwind CSS standalone binary: you only need PHP.

## How to add a page?

Create a Markdown file in `pages/docs/` (or in one of its sub-folders): it is automatically added to the sidebar. See [Getting started](page:docs/introduction/getting-started).

## How to order pages and groups?

Use a number prefix in the file name of a page (e.g. `1-intro.md`), or the `weight` front matter variable. For a group, set `weight` in its `index.md` file. See [Navigation](page:docs/guides/navigation).

## How to enable search?

Set `docsearch.enabled` to `true` and provide your Algolia credentials, or install the FlexSearch component theme for a local search. See [Site Search](page:docs/guides/search).

## How to disable the second language?

Set `enabled: false` on the language in the `languages` section of `cecil.yml`. See [Internationalization](page:docs/guides/internationalization).

## Where to deploy my site?

Anywhere: the generated `_site/` directory contains only static files (HTML, CSS, JavaScript, images). Netlify, Vercel, GitHub Pages, GitLab Pages or any web server will do.

## Something is not working?

Please [open an issue on GitHub](https://github.com/Cecilapp/statidocs/issues/new/choose).
