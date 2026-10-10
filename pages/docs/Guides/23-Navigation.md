---
title: Navigation
description: How the sidebar, breadcrumb and previous/next links are built from your pages.
---
# Navigation

The navigation of the documentation is generated automatically from the folders structure of `pages/docs/`: there is nothing to configure.

## Sidebar

The sidebar is built from [nested sections](https://cecil.app/documentation/content/#sub-section): each sub-folder containing an `index.md` file becomes a collapsible group, at any depth.

```text
pages/docs/
├─ index.md            → /docs/
├─ 1-getting-started.md
└─ guides/
   ├─ index.md         → group "Guides"
   ├─ 1-notes.md
   └─ advanced/
      ├─ index.md      → group "Advanced", inside "Guides"
      └─ 1-customization.md
```

The `index.md` file of a group defines its title, its description and its position, and its content is displayed on the group page, followed by the list of its pages:

```yaml
---
title: Guides
description: Tutorials and instructions.
weight: 20
---
Guides are a set of tutorials to help you understand how to use Statidocs.
```

## Ordering

Pages and groups are sorted by `weight` (ascending):

- for a page, use a number prefix in its file name (e.g. `1-getting-started.md`) or the `weight` front matter variable;
- for a group, use the `weight` front matter variable in its `index.md` file.

:::important
The number prefix is removed from file names only: a prefix on a folder name would be kept in its URL. Use the `weight` front matter variable to order groups.
:::

## Collapsed groups

Groups are open by default. To collapse a group, set `collapsed: true` in the front matter of its `index.md` file:

```yaml
---
title: Advanced
collapsed: true
---
```

To collapse all groups, use the `sidebar.collapsed` option in the configuration:

```yaml
sidebar:
  collapsed: true
```

:::info
The group of the current page is always open.
:::

## Breadcrumb and previous/next links

Each documentation page displays a breadcrumb (based on its ancestors) and links to the previous and next pages, following the order of the sidebar, through nested groups.

## Table of contents

The “On this page” table of contents is generated from the headings (`##`, `###`) of the page, and highlights the current section while scrolling.

## Header and footer menus

The `main` menu is displayed in the header (and in the sidebar on mobile), and the optional `footer` menu in the footer:

```yaml
menus:
  main:
    - id: docs
      name: Documentation
      url: /docs/
      weight: 10
  footer:
    - id: cecil
      name: Cecil
      url: https://cecil.app
```

A page can also be added to a menu from its front matter:

```yaml
---
title: About
menu:
  main:
    weight: 999
---
```

:::tip
See the [Cecil menus documentation](https://cecil.app/documentation/configuration/#menus) for more details.
:::
