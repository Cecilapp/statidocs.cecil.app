---
title: Référence de la configuration
description: Options de configuration de Statidocs et du thème Docs.
---
# Référence de la configuration

La configuration de votre site est définie dans le fichier `cecil.yml`. Statidocs prend en charge toutes les [options de configuration de Cecil](https://cecil.app/documentation/configuration/), ainsi que les options suivantes du thème _Docs_.

## Site

| Option        | Description                                                              | Défaut                   |
|---------------|--------------------------------------------------------------------------|--------------------------|
| `title`       | Titre du site, affiché dans l’en-tête et sur la page d’accueil.          |                          |
| `baseline`    | Slogan court, affiché sur la page d’accueil.                             |                          |
| `description` | Description du site, utilisée dans les balises meta.                     |                          |
| `author`      | Auteur du site (`name`, `url`).                                          |                          |
| `logo`        | Image du logo (dans `assets/`), ou images `light` et `dark`.             |                          |
| `footer`      | Texte du pied de page (`%author%` est remplacé par le nom de l’auteur).  | `Copyright © %author%`   |

## Navigation

| Option              | Description                                                                 | Défaut  |
|---------------------|-----------------------------------------------------------------------------|---------|
| `menus.main`        | Entrées du menu d’en-tête.                                                  |         |
| `menus.footer`      | Entrées du menu de pied de page.                                            |         |
| `sidebar.collapsed` | Replie les groupes de la barre latérale, sauf celui de la page courante.    | `false` |

## Pages

| Option            | Description                                                                                  | Défaut  |
|-------------------|----------------------------------------------------------------------------------------------|---------|
| `lastupdated`     | Affiche la date de la page comme date de « Mise à jour » (`updated` est toujours affiché).   | `false` |
| `language_cookie` | Nom d’un cookie enregistrant la langue choisie avec le sélecteur (par exemple `nf_lang`).    | `false` |

## Versions

| Option     | Description                                                                               | Défaut               |
|------------|-------------------------------------------------------------------------------------------|----------------------|
| `versions` | Versions de la documentation (`name`, `url`), affichées dans un sélecteur de l’en-tête.   |                      |
| `version`  | Nom de la version courante.                                                               | la première version  |

## GitHub

| Option          | Description                                                | Défaut  |
|-----------------|------------------------------------------------------------|---------|
| `github.url`    | URL du dépôt, liée dans l’en-tête.                         |         |
| `github.repo`   | URL du dépôt utilisée par le lien « Modifier cette page ». |         |
| `github.branch` | Branche du dépôt.                                          | `main`  |
| `github.path`   | Chemin du répertoire des pages dans le dépôt.              | `pages` |

## Recherche

Les options de recherche sont fournies par les thèmes composants [DocSearch](https://github.com/Cecilapp/theme-docsearch) et [FlexSearch](https://github.com/Cecilapp/theme-flexsearch), qui doivent être installés et ajoutés à la section `theme`. Consultez [Recherche sur le site](page:fr/docs/guides/search).

| Option                 | Description                                                  | Défaut  |
|------------------------|--------------------------------------------------------------|---------|
| `docsearch.enabled`    | Affiche le champ de recherche DocSearch.                     | `true`  |
| `docsearch.appId`      | Identifiant de l’application Algolia.                        |         |
| `docsearch.indexName`  | Nom de l’index Algolia.                                      |         |
| `docsearch.apiKey`     | Clé d’API Algolia de recherche uniquement.                   |         |
| `docsearch.language`   | Filtre les résultats sur la langue courante.                 | `true`  |
| `docsearch.insights`   | Active Algolia Insights.                                     | `false` |
| `docsearch.debug`      | Garde la fenêtre de recherche ouverte (pour le débogage).    | `false` |
| `flexsearch.enabled`   | Affiche le champ de recherche FlexSearch.                    | `true`  |
| `flexsearch.sections`  | Sections indexées, dans l’ordre des groupes de résultats.    | toutes  |

## Exemple

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
  - docsearch
  - pwa
```
