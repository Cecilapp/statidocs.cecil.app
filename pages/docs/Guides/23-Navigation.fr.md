---
title: Navigation
description: Comment la barre latérale, le fil d’Ariane et les liens précédent/suivant sont construits à partir de vos pages.
---
# Navigation

La navigation de la documentation est générée automatiquement à partir de la structure des répertoires de `pages/docs/` : il n’y a rien à configurer.

## Barre latérale

La barre latérale est construite à partir des [sections imbriquées](https://cecil.app/documentation/content/#sub-section) : chaque sous-répertoire contenant un fichier `index.md` devient un groupe repliable, quelle que soit sa profondeur.

```text
pages/docs/
├─ index.md            → /docs/
├─ 1-getting-started.md
└─ guides/
   ├─ index.md         → groupe « Guides »
   ├─ 1-notes.md
   └─ advanced/
      ├─ index.md      → groupe « Advanced », dans « Guides »
      └─ 1-customization.md
```

Le fichier `index.md` d’un groupe définit son titre, sa description et sa position ; son contenu est affiché sur la page du groupe, suivi de la liste de ses pages :

```yaml
---
title: Guides
description: Tutoriels et instructions.
weight: 20
---
Les guides sont un ensemble de tutoriels pour vous aider à comprendre comment utiliser Statidocs.
```

## Ordre

Les pages et les groupes sont triés par `weight` (poids, par ordre croissant) :

- pour une page, utilisez un préfixe numérique dans le nom du fichier (par exemple `1-getting-started.md`) ou la variable de front matter `weight` ;
- pour un groupe, utilisez la variable de front matter `weight` dans son fichier `index.md`.

:::important
Le préfixe numérique n’est retiré que des noms de fichiers : un préfixe sur un nom de répertoire serait conservé dans son URL. Utilisez la variable de front matter `weight` pour ordonner les groupes.
:::

## Groupes repliés

Les groupes sont ouverts par défaut. Pour replier un groupe, définissez `collapsed: true` dans le front matter de son fichier `index.md` :

```yaml
---
title: Advanced
collapsed: true
---
```

Pour replier tous les groupes, utilisez l’option `sidebar.collapsed` dans la configuration :

```yaml
sidebar:
  collapsed: true
```

:::info
Le groupe de la page courante est toujours ouvert.
:::

## Fil d’Ariane et liens précédent/suivant

Chaque page de documentation affiche un fil d’Ariane (basé sur ses ancêtres) et des liens vers les pages précédente et suivante, en suivant l’ordre de la barre latérale, à travers les groupes imbriqués.

## Table des matières

La table des matières « Sur cette page » est générée à partir des titres (`##`, `###`) de la page et met en évidence la section courante pendant le défilement.

## Menus d’en-tête et de pied de page

Le menu `main` est affiché dans l’en-tête (et dans la barre latérale sur mobile), et le menu facultatif `footer` dans le pied de page :

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

Une page peut également être ajoutée à un menu depuis son front matter :

```yaml
---
title: About
menu:
  main:
    weight: 999
---
```

:::tip
Consultez la [documentation de Cecil sur les menus](https://cecil.app/documentation/configuration/#menus) pour plus de détails.
:::
