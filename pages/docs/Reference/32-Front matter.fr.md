---
title: Référence du front matter
description: Variables de front matter prises en charge par les pages de Statidocs.
---
# Référence du front matter

Le front matter est un bloc YAML, en haut d’un fichier Markdown, qui définit les variables de la page. Statidocs prend en charge toutes les [variables de page de Cecil](https://cecil.app/documentation/content/#variables), ainsi que les variables suivantes du thème _Docs_.

```yaml
---
title: Getting started
description: Learn how to start building your documentation website.
weight: 10
updated: 2026-10-01
---
```

## Pages

| Variable      | Description                                                                              |
|---------------|------------------------------------------------------------------------------------------|
| `title`       | Titre de la page, affiché dans la barre latérale, le fil d’Ariane et l’onglet du navigateur. |
| `description` | Description de la page, utilisée dans les balises meta et dans la liste des pages d’un groupe. |
| `weight`      | Position de la page dans la barre latérale (ou utilisez un préfixe numérique dans le nom du fichier). |
| `updated`     | Date de « Mise à jour » de la page (`AAAA-MM-JJ`).                                       |
| `date`        | Date de la page, affichée comme date de « Mise à jour » lorsque `lastupdated` est activé. |
| `menu`        | Ajoute la page à un menu (par exemple `menu: main`).                                     |
| `draft`       | Si `true`, la page n’est pas publiée.                                                    |

## Groupes

Variables du fichier `index.md` d’un groupe de la barre latérale (sous-répertoire de `pages/docs/`) :

| Variable      | Description                                                                         |
|---------------|-------------------------------------------------------------------------------------|
| `title`       | Titre du groupe (traduisible via les fichiers de traduction).                       |
| `description` | Description du groupe.                                                              |
| `weight`      | Position du groupe dans la barre latérale.                                          |
| `collapsed`   | Si `true`, le groupe est replié (sauf s’il contient la page courante).              |

## Page d’accueil

| Variable | Description                                                                                                  |
|----------|--------------------------------------------------------------------------------------------------------------|
| `blocks` | Liste des blocs de la page d’accueil (`hero`, `cta`, `features`) : voir [Personnalisation](page:fr/docs/guides/customization). |

## Articles de blog

Si vous ajoutez une section `blog`, les articles affichent leur date, leur temps de lecture et leur(s) auteur(s) :

| Variable              | Description                                                                         |
|-----------------------|-------------------------------------------------------------------------------------|
| `author` ou `authors` | Un objet (`name`, `title`, `url`, `email`, `image`) ou une clé de `data/authors.yml`. |
