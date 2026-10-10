---
title: Recherche sur le site
description: Ajoutez une recherche à Statidocs avec le thème composant Algolia DocSearch ou FlexSearch.
---
# Recherche sur le site

Statidocs propose deux solutions de recherche, chacune fournie sous forme de [thème composant](https://cecil.app/documentation/themes/) dédié et accessible via un bouton dans l’en-tête :

- [Algolia DocSearch](#algolia-docsearch) : un service de recherche hébergé, gratuit pour les projets open source ;
- [FlexSearch](#flexsearch) : un index de recherche local, généré avec votre site, sans aucun service externe.

Les deux ouvrent une fenêtre de recherche avec le raccourci `Ctrl`/`⌘` + `K`, prennent en charge la navigation au clavier et sont traduits en anglais et en français.

:::info
DocSearch est prioritaire si les deux sont installés et activés.
:::

## Algolia DocSearch

Le [thème composant DocSearch](https://github.com/Cecilapp/theme-docsearch) interroge un index Algolia de votre site.

Le service est gratuit pour tout projet open source : [inscrivez-vous au programme DocSearch](https://docsearch.algolia.com/apply/). DocSearch explore votre site périodiquement et regroupe son contenu dans un index Algolia, qui est ensuite interrogé directement depuis votre interface avec l’API Algolia.

:::info
Si votre site n’est [pas éligible](https://docsearch.algolia.com/docs/who-can-apply/) au programme gratuit ou s’il se trouve derrière un pare-feu, vous pouvez [exécuter votre propre](https://www.algolia.com/doc/tools/crawler/getting-started/overview/) explorateur.
:::

### Installation de DocSearch

```bash
composer require cecil/theme-docsearch
```

Ajoutez-le ensuite après `docs` dans la section `theme` de la configuration, avec vos identifiants Algolia :

```yaml
theme:
  - docs
  - docsearch
docsearch:
  appId: <YOUR_APP_ID>
  indexName: <YOUR_INDEX_NAME>
  apiKey: <YOUR_SEARCH_API_KEY>
```

:::warning
Utilisez la clé d’API **de recherche uniquement** : elle est publiée dans le HTML des pages.
:::

### Configuration de DocSearch

Principales options (valeurs par défaut) :

```yaml
docsearch:
  enabled: true # affiche le champ de recherche
  appId: '' # identifiant de l’application Algolia
  indexName: '' # nom de l’index Algolia
  apiKey: '' # clé d’API de recherche Algolia
  language: true # filtre les résultats sur la langue courante (facette `lang`)
  insights: false # envoie les événements de recherche à Algolia Insights
  debug: false # garde la fenêtre ouverte lors de la perte du focus
  placeholder: '' # texte indicatif du champ de recherche
  search_parameters: {} # paramètres de recherche Algolia supplémentaires
```

Consultez la [documentation du thème composant DocSearch](https://github.com/Cecilapp/theme-docsearch#configuration) pour l’ensemble des options.

:::tip
Les résultats sont filtrés sur la langue courante, à partir de la balise meta `docsearch:language` ajoutée à chaque page. Définissez `language: false` si votre index n’a pas de facette `lang`.
:::

### Configuration de l’explorateur

Lorsque votre site est accepté dans le programme DocSearch, Algolia crée une configuration d’exploration par défaut, modifiable dans le [tableau de bord du Crawler](https://crawler.algolia.com).

Avec le thème Docs, l’extracteur d’enregistrements recommandé est :

```js
recordExtractor: ({ helpers }) => {
  return helpers.docsearch({
    recordProps: {
      lvl0: {
        selectors: "#sidebar li>a.active",
        defaultValue: "Documentation",
      },
      lvl1: ["article h1"],
      lvl2: ["article h2"],
      lvl3: ["article h3"],
      lvl4: ["article h4"],
      lvl5: ["article h5"],
      lvl6: ["article h6"],
      content: ["#content p, #content li"],
    },
    aggregateContent: true,
    recordVersion: "v3",
  });
},
```

Déclarez `lang` dans les `attributesForFaceting` des réglages de l’index, pour filtrer les résultats par langue :

```js
initialIndexSettings: {
  "<YOUR_INDEX_NAME>": {
    attributesForFaceting: ["type", "lang"],
    // ...
  },
},
```

Consultez le [guide de configuration de l’explorateur](https://github.com/Cecilapp/theme-docsearch/blob/main/docs/crawler.md) pour un exemple complet.

## FlexSearch

Comme alternative à DocSearch (sans service externe ni explorateur), le [thème composant FlexSearch](https://github.com/Cecilapp/theme-flexsearch) génère un index de recherche lors de la génération du site (un fichier JSON statique par langue), chargé à la première utilisation.

### Installation de FlexSearch

```bash
composer require cecil/theme-flexsearch
```

Ajoutez-le ensuite après `docs` dans la section `theme` de la configuration :

```yaml
theme:
  - docs
  - flexsearch
```

:::tip
Si DocSearch est également installé, désactivez-le (`docsearch.enabled: false`) pour utiliser FlexSearch.
:::

### Configuration de FlexSearch

Les résultats sont regroupés par section, dans l’ordre de `flexsearch.sections` (toutes les sections racines sont indexées par défaut) :

```yaml
flexsearch:
  sections:
    docs:
      limit: 5 # nombre maximum de résultats dans le groupe
```

Options des sections :

| Option   | Description                                                                 | Défaut                       |
|----------|-----------------------------------------------------------------------------|------------------------------|
| `title`  | Titre du groupe de résultats.                                               | titre de la page de section  |
| `limit`  | Nombre maximum de résultats affichés dans le groupe.                        | `5`                          |
| `split`  | Un enregistrement par titre `<h2>`/`<h3>`, ou un seul par page.             | `true`                       |
| `date`   | Affiche la date de la page dans les résultats.                              | `false`                      |
| `length` | Longueur maximale du texte indexé d’une page non découpée.                  | `1000`                       |

Autres options (valeurs par défaut) :

```yaml
flexsearch:
  enabled: true # affiche le champ de recherche
  trigger: auto # bouton : auto (icône seule sur mobile), icon ou full
  hotkey: k # Ctrl/⌘ + touche ouvre la recherche (false pour désactiver)
  credit: true # affiche la mention « Search by FlexSearch »
  suggest: true # recherche approximative si aucun résultat exact
```

Consultez la [documentation du thème composant FlexSearch](https://github.com/Cecilapp/theme-flexsearch#configuration) pour l’ensemble des options (tokenisation, encodeur, poids des champs, etc.).

:::info
Les pages exclues des listes (`exclude: true`) ne sont pas indexées.
:::
