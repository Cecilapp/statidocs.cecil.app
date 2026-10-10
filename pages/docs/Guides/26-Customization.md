---
title: Customization
description: Customize the logo, the homepage, the footer and the templates of your Statidocs site.
---
# Customization

Most of the appearance of Statidocs is controlled from the configuration (`cecil.yml`) and the front matter of the homepage. For deeper changes, you can override the templates of the theme.

## Title and logo

The site title is displayed in the header, with an optional logo: an image of the `assets/` directory, single or one per color theme.

```yaml
title: My project
baseline: The documentation of my project
logo: logo.png
# or
logo:
  light: logo-light.png
  dark: logo-dark.png
```

## Homepage

The homepage (`pages/index.md`) is built from blocks, listed in its front matter, followed by its content:

```yaml
---
blocks:
  - name: hero # site title and baseline
    description: A **Markdown** text.
    image: hero.svg # optional
  - name: cta # call to action
    button: # optional: first page of the documentation by default
      title: Get started
      url: /docs/
    links:
      - title: GitHub
        url: https://github.com/<org>/<repo>
  - name: features
    features:
      - title: Feature 1
        description: A **Markdown** text.
      - title: Feature 2
        description: A **Markdown** text.
---
Content displayed below the blocks.
```

| Block      | Description                                                                 |
|------------|-----------------------------------------------------------------------------|
| `hero`     | Site title and baseline, a Markdown `description` and an optional `image`.  |
| `cta`      | A button (the first documentation page by default) and a list of `links`.   |
| `features` | A grid of `features`, each with a `title` and a Markdown `description`.     |

## Footer

The footer displays a text, with the `%author%` placeholder replaced by the author name, and the optional `footer` menu (see [Navigation](page:docs/guides/navigation)):

```yaml
author:
  name: Arnaud Ligny
  url: https://arnaudligny.fr
footer: Copyright © %author%
```

## GitHub links

The `github` options add a link to the repository in the header, and an “Edit this page” link at the bottom of each documentation page:

```yaml
github:
  url: https://github.com/<org>/<repo> # GitHub link in header
  repo: https://github.com/<org>/<repo> # "Edit this page" link
  branch: main
  path: pages # pages directory path in the repository (default: pages)
```

## Last updated date

The `updated` front matter variable of a page is displayed as its “Last updated” date:

```yaml
---
title: FAQ
updated: 2026-10-01
---
```

To display the date of all pages (from the `date` front matter variable or the file modification date), enable the `lastupdated` option:

```yaml
lastupdated: true
```

## Dark mode

The color theme follows the system preference, with a manual toggle in the header (light, dark or system). Images are slightly dimmed in dark mode.

## Progressive Web App

Statidocs includes the [PWA theme](https://github.com/Cecilapp/theme-pwa): a web manifest and a service worker, to make your documentation installable and available offline.

```yaml
manifest:
  background_color: '#1C4ED8'
  theme_color: '#1C4ED8'
serviceworker:
  enabled: true
```

## Override templates

To change the HTML of a part of the site, create a template with the same path in your `layouts/` directory: it takes precedence over the one of the theme. For example, to change the logo, create `layouts/partials/logo.html.twig`.

Main templates of the _Docs_ theme:

- `_default/home.html.twig` — Homepage
- `docs/page.html.twig` and `docs/list.html.twig` — Documentation pages and groups
- `_default/404.html.twig` — Page not found
- `partials/blocks/*.html.twig` — Homepage blocks (you can add your own block)
- `partials/sidebar-nav.html.twig` — Sidebar navigation

:::tip
Browse the [theme source code](https://github.com/Cecilapp/theme-docs/tree/main/layouts) and read the [Cecil templates documentation](https://cecil.app/documentation/templates/).
:::
