---
title: Mise en route
description: Découvrez comment commencer à créer votre site de documentation avec Statidocs, propulsé par Cecil.
---
# Mise en route

Statidocs est un starter de documentation, construit avec le générateur de site statique [Cecil](https://cecil.app) et son [thème _Docs_](https://github.com/Cecilapp/theme-docs).

:::important
PHP 8.3+ est requis.
:::

## Créer un nouveau projet

La façon la plus simple de créer un nouveau projet Statidocs est d’utiliser [Composer](https://getcomposer.org) :

```bash
composer create-project cecil/statidocs --ask
```

:::info
Cette commande télécharge également le binaire `cecil.phar` dans le répertoire de votre projet.
:::

## Démarrer le serveur local

En local, le [serveur intégré de Cecil](https://cecil.app/documentation/commands/#serve) vous permet de prévisualiser votre travail et rafraîchit automatiquement votre navigateur lorsque vous faites des modifications.

Dans le répertoire de votre projet, lancez la commande suivante pour démarrer le serveur local :

```bash
php cecil.phar serve
```

Un message indiquant l’URL de la prévisualisation locale s’affiche dans votre terminal. Ouvrez cette URL (<http://localhost:8000> par défaut) pour parcourir votre documentation.

## Ajouter des pages

### Formats de fichiers

Statidocs prend en charge la rédaction de contenu en Markdown sans aucune configuration. Vous pouvez étendre les capacités par défaut en activant les [options Markdown de Cecil](https://cecil.app/documentation/content/#markdown).

### Organiser les pages

Ajoutez de nouvelles pages à votre site en créant des fichiers `.md` dans `pages/docs/`. Utilisez des sous-répertoires pour regrouper les pages : chaque sous-répertoire contenant un fichier `index.md` devient un groupe repliable dans la barre latérale, quelle que soit sa profondeur.

Par exemple, la structure de fichiers suivante génère les pages `/docs/getting-started/`, `/docs/guides/i18n/` et `/docs/guides/advanced/customization/` :

```text
<my-project>
└─ pages
   └─ docs
      ├─ 1-Getting started.md
      └─ guides
         ├─ index.md
         ├─ 2-i18n.md
         └─ advanced
            ├─ index.md
            └─ 1-customization.md
```

Les pages sont triées par `weight` (poids) : utilisez un préfixe numérique dans le nom du fichier (par exemple `1-`) ou la variable de front matter `weight`.

:::tip
Pour en savoir plus sur la barre latérale, consultez le [guide Navigation](page:fr/docs/guides/navigation).
:::

### Front matter

Toutes les pages utilisent des variables de front matter pour contrôler leur affichage :

```yaml
---
title: Hello world
description: This is a page description.
---
```

Consultez la [référence du front matter](page:fr/docs/reference/front-matter) pour la liste complète des variables.

## Générer et déployer

Lorsque vous êtes prêt à publier, générez le site statique dans le répertoire `_site/` :

```bash
php cecil.phar build
```

Envoyez ensuite le contenu de `_site/` sur n’importe quel hébergeur de sites statiques (Netlify, Vercel, GitHub Pages, etc.). Consultez la [documentation de déploiement de Cecil](https://cecil.app/documentation/deploy/) pour plus de détails.

## Mettre à jour Statidocs

Statidocs est construit sur le thème Cecil _[Docs](https://github.com/Cecilapp/theme-docs)_. Vous pouvez le mettre à jour, ainsi que les autres thèmes Cecil, en lançant la commande suivante dans votre terminal :

```bash
composer update
```

Mettez à jour Cecil lui-même avec sa commande `self-update` :

```bash
php cecil.phar self-update
```
