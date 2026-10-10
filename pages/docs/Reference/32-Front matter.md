---
title: Front matter reference
description: Front matter variables supported by the pages of Statidocs.
---
# Front matter reference

The front matter is a YAML block, at the top of a Markdown file, used to define the variables of the page. Statidocs supports all [Cecil page variables](https://cecil.app/documentation/content/#variables), plus the following variables of the _Docs_ theme.

```yaml
---
title: Getting started
description: Learn how to start building your documentation website.
weight: 10
updated: 2026-10-01
---
```

## Pages

| Variable      | Description                                                                  |
|---------------|------------------------------------------------------------------------------|
| `title`       | Page title, displayed in the sidebar, the breadcrumb and the browser tab.    |
| `description` | Page description, used in meta tags and in the list of pages of a group.     |
| `weight`      | Position of the page in the sidebar (or use a number prefix in the filename). |
| `updated`     | “Last updated” date of the page (`YYYY-MM-DD`).                              |
| `date`        | Page date, displayed as “Last updated” date when `lastupdated` is enabled.   |
| `menu`        | Adds the page to a menu (e.g. `menu: main`).                                 |
| `draft`       | If `true`, the page is not published.                                        |

## Groups

Variables of the `index.md` file of a sidebar group (sub-folder of `pages/docs/`):

| Variable      | Description                                                          |
|---------------|----------------------------------------------------------------------|
| `title`       | Group title (translatable through the translations files).          |
| `description` | Group description.                                                   |
| `weight`      | Position of the group in the sidebar.                                |
| `collapsed`   | If `true`, the group is collapsed (except when it contains the current page). |

## Homepage

| Variable | Description                                                                                       |
|----------|---------------------------------------------------------------------------------------------------|
| `blocks` | List of homepage blocks (`hero`, `cta`, `features`): see [Customization](page:docs/guides/customization). |

## Blog posts

If you add a `blog` section, posts display their date, reading time and author(s):

| Variable              | Description                                                                         |
|-----------------------|-------------------------------------------------------------------------------------|
| `author` or `authors` | An object (`name`, `title`, `url`, `email`, `image`) or a key of `data/authors.yml`. |
