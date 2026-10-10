---
title: Personnalisation
description: Personnalisez le logo, la page d’accueil, le pied de page et les templates de votre site Statidocs.
---
# Personnalisation

L’essentiel de l’apparence de Statidocs se contrôle depuis la configuration (`cecil.yml`) et le front matter de la page d’accueil. Pour des changements plus profonds, vous pouvez surcharger les templates du thème.

## Titre et logo

Le titre du site est affiché dans l’en-tête, avec un logo facultatif : une image du répertoire `assets/`, unique ou une par thème de couleur.

```yaml
title: My project
baseline: The documentation of my project
logo: logo.png
# or
logo:
  light: logo-light.png
  dark: logo-dark.png
```

## Page d’accueil

La page d’accueil (`pages/index.md`) est construite à partir de blocs, listés dans son front matter, suivis de son contenu :

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
Contenu affiché sous les blocs.
```

| Bloc       | Description                                                                          |
|------------|--------------------------------------------------------------------------------------|
| `hero`     | Titre et slogan du site, une `description` en Markdown et une `image` facultative.   |
| `cta`      | Un bouton (la première page de la documentation par défaut) et une liste de `links`. |
| `features` | Une grille de `features`, chacune avec un `title` et une `description` en Markdown.  |

## Pied de page

Le pied de page affiche un texte, dans lequel `%author%` est remplacé par le nom de l’auteur, ainsi que le menu facultatif `footer` (voir [Navigation](page:fr/docs/guides/navigation)) :

```yaml
author:
  name: Arnaud Ligny
  url: https://arnaudligny.fr
footer: Copyright © %author%
```

## Liens GitHub

Les options `github` ajoutent un lien vers le dépôt dans l’en-tête, ainsi qu’un lien « Modifier cette page » en bas de chaque page de documentation :

```yaml
github:
  url: https://github.com/<org>/<repo> # GitHub link in header
  repo: https://github.com/<org>/<repo> # "Edit this page" link
  branch: main
  path: pages # pages directory path in the repository (default: pages)
```

## Date de mise à jour

La variable de front matter `updated` d’une page est affichée comme sa date de « Mise à jour » :

```yaml
---
title: FAQ
updated: 2026-10-01
---
```

Pour afficher la date de toutes les pages (issue de la variable de front matter `date` ou de la date de modification du fichier), activez l’option `lastupdated` :

```yaml
lastupdated: true
```

## Mode sombre

Le thème de couleur suit la préférence du système, avec un sélecteur manuel dans l’en-tête (clair, sombre ou système). Les images sont légèrement assombries en mode sombre.

## Progressive Web App

Statidocs inclut le [thème PWA](https://github.com/Cecilapp/theme-pwa) : un manifeste web et un service worker, pour rendre votre documentation installable et disponible hors ligne.

```yaml
manifest:
  background_color: '#1C4ED8'
  theme_color: '#1C4ED8'
serviceworker:
  enabled: true
```

## Surcharger les templates

Pour modifier le HTML d’une partie du site, créez un template avec le même chemin dans votre répertoire `layouts/` : il est prioritaire sur celui du thème. Par exemple, pour modifier le logo, créez `layouts/partials/logo.html.twig`.

Principaux templates du thème _Docs_ :

- `_default/home.html.twig` — Page d’accueil
- `docs/page.html.twig` et `docs/list.html.twig` — Pages et groupes de la documentation
- `_default/404.html.twig` — Page introuvable
- `partials/blocks/*.html.twig` — Blocs de la page d’accueil (vous pouvez ajouter votre propre bloc)
- `partials/sidebar-nav.html.twig` — Navigation de la barre latérale

:::tip
Parcourez le [code source du thème](https://github.com/Cecilapp/theme-docs/tree/main/layouts) et lisez la [documentation de Cecil sur les templates](https://cecil.app/documentation/templates/).
:::
