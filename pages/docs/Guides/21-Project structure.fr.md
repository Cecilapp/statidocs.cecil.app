---
title: Structure du projet
description: Ce guide vous montre comment est organisé un projet Statidocs et à quoi servent les différents fichiers de votre projet.
---
# Structure du projet

Ce guide vous montre comment est organisé un projet Statidocs et à quoi servent les différents fichiers de votre projet.

Les projets Statidocs suivent la même structure de fichiers et de répertoires que les projets Cecil. Consultez la [documentation de Cecil sur l’organisation des fichiers](https://cecil.app/documentation/content/#files-organization) pour plus de détails.

## Exemple

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

## Fichiers et répertoires

- `cecil.yml` — Le fichier de [configuration](page:fr/docs/reference/configuration).
- `composer.json` — Les dépendances du projet : thèmes Cecil (_Docs_, _PWA_, etc.).
- `pages/` — Le contenu de votre site, rédigé en Markdown :
  - `pages/index.md` — La page d’accueil, construite à partir de [blocs](page:fr/docs/guides/customization) définis dans son front matter.
  - `pages/docs/` — Chaque fichier Markdown (`.md`) de ce répertoire est transformé en page de documentation ; chaque sous-répertoire contenant un fichier `index.md` devient un [groupe de la barre latérale](page:fr/docs/guides/navigation).
- `assets/` — Les ressources (styles, images, favicon, PDF, etc.) qui seront traitées (redimensionnées, optimisées, empreintées, etc.).
- `static/` (facultatif) — Les fichiers copiés tels quels dans le site généré.
- `data/` (facultatif) — Les fichiers de données (YAML, JSON, CSV, etc.) disponibles dans les templates, comme la liste des auteurs.
- `layouts/` (facultatif) — Vos propres templates [Twig](https://twig.symfony.com), pour surcharger ceux du thème.
- `themes/` — Les thèmes installés, gérés par Composer : ne les modifiez pas directement.
- `translations/` (facultatif) — Les données de traduction nécessaires à l’[internationalisation](page:fr/docs/guides/internationalization).

:::info
Le répertoire `_site/` (site généré) et le répertoire `.cache/` sont créés par Cecil : il n’est pas nécessaire de les versionner.
:::
