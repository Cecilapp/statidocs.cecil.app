---
title: FAQ
description: Questions fréquentes sur Statidocs.
---
# FAQ

## Quelle est la différence entre Statidocs et le thème Docs ?

Le [thème _Docs_](https://github.com/Cecilapp/theme-docs) fournit les templates et les styles. Statidocs est un projet prêt à l’emploi (configuration, structure des pages, traductions, PWA) construit dessus : le moyen le plus rapide de démarrer un site de documentation avec [Cecil](https://cecil.app).

## Node.js est-il nécessaire ?

Non. Cecil est une application PHP, et le CSS du thème est compilé avec le binaire autonome de Tailwind CSS : seul PHP est nécessaire.

## Comment ajouter une page ?

Créez un fichier Markdown dans `pages/docs/` (ou dans l’un de ses sous-répertoires) : il est automatiquement ajouté à la barre latérale. Consultez [Mise en route](page:fr/docs/introduction/getting-started).

## Comment ordonner les pages et les groupes ?

Utilisez un préfixe numérique dans le nom du fichier d’une page (par exemple `1-intro.md`) ou la variable de front matter `weight`. Pour un groupe, définissez `weight` dans son fichier `index.md`. Consultez [Navigation](page:fr/docs/guides/navigation).

## Comment activer la recherche ?

Installez le thème composant DocSearch (`composer require cecil/theme-docsearch`) et renseignez vos identifiants Algolia, ou installez le thème composant FlexSearch (`composer require cecil/theme-flexsearch`) pour une recherche locale, puis ajoutez-le à la section `theme`. Consultez [Recherche sur le site](page:fr/docs/guides/search).

## Comment désactiver la seconde langue ?

Définissez `enabled: false` sur la langue, dans la section `languages` de `cecil.yml`. Consultez [Internationalisation](page:fr/docs/guides/internationalization).

## Où déployer mon site ?

N’importe où : le répertoire `_site/` généré ne contient que des fichiers statiques (HTML, CSS, JavaScript, images). Netlify, Vercel, GitHub Pages, GitLab Pages ou n’importe quel serveur web feront l’affaire.

## Quelque chose ne fonctionne pas ?

Merci d’[ouvrir une issue sur GitHub](https://github.com/Cecilapp/statidocs/issues/new/choose).
