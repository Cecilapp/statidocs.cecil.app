---
title: Configuration reference
description: Configuration options of Statidocs and of the Docs theme.
---
# Configuration reference

The configuration of your site is defined in the `cecil.yml` file. Statidocs supports all [Cecil configuration options](https://cecil.app/documentation/configuration/), plus the following options of the _Docs_ theme.

## Site

| Option        | Description                                                         | Default                  |
|---------------|---------------------------------------------------------------------|--------------------------|
| `title`       | Site title, displayed in the header and on the homepage.            |                          |
| `baseline`    | Short tagline, displayed on the homepage.                           |                          |
| `description` | Site description, used in meta tags.                                |                          |
| `author`      | Site author (`name`, `url`).                                        |                          |
| `logo`        | Logo image (in `assets/`), or `light` and `dark` images.            |                          |
| `footer`      | Footer text (`%author%` is replaced by the author name).            | `Copyright © %author%`   |

## Navigation

| Option              | Description                                                                 | Default |
|---------------------|-----------------------------------------------------------------------------|---------|
| `menus.main`        | Header menu entries.                                                        |         |
| `menus.footer`      | Footer menu entries.                                                        |         |
| `sidebar.collapsed` | Collapse the sidebar groups, except the one of the current page.            | `false` |

## Pages

| Option            | Description                                                                         | Default |
|-------------------|-------------------------------------------------------------------------------------|---------|
| `lastupdated`     | Display the page date as “Last updated” date (`updated` is always displayed).       | `false` |
| `language_cookie` | Name of a cookie storing the language chosen with the selector (e.g. `nf_lang`).    | `false` |

## GitHub

| Option          | Description                                         | Default |
|-----------------|-----------------------------------------------------|---------|
| `github.url`    | Repository URL, linked in the header.               |         |
| `github.repo`   | Repository URL used by the “Edit this page” link.   |         |
| `github.branch` | Branch of the repository.                           | `main`  |
| `github.path`   | Path of the pages directory in the repository.      | `pages` |

## Search

| Option                | Description                                          | Default |
|-----------------------|------------------------------------------------------|---------|
| `docsearch.enabled`   | Enable [Algolia DocSearch](page:docs/guides/search). | `false` |
| `docsearch.appId`     | Algolia application ID.                              |         |
| `docsearch.indexName` | Algolia index name.                                  |         |
| `docsearch.apiKey`    | Algolia search API key.                              |         |
| `docsearch.insights`  | Enable Algolia Insights.                             | `false` |
| `docsearch.debug`     | Keep the search modal open (for debugging).          | `false` |
| `flexsearch`          | Options of the FlexSearch component theme.           |         |

## Example

```yaml
title: Statidocs
baseline: Build a documentation website quickly
baseurl: https://statidocs.cecil.app/
author:
  name: Arnaud Ligny
  url: https://arnaudligny.fr
logo: logo.png
footer: Copyright © %author%
menus:
  main:
    - id: docs
      weight: 0
github:
  url: https://github.com/Cecilapp/statidocs
  repo: https://github.com/Cecilapp/statidocs.cecil.app
  branch: main
sidebar:
  collapsed: false
lastupdated: false
docsearch:
  enabled: true
  appId: <YOUR_APP_ID>
  indexName: <YOUR_INDEX_NAME>
  apiKey: <YOUR_SEARCH_API_KEY>
theme:
  - docs
  - pwa
```
