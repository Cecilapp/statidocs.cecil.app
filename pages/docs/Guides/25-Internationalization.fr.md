---
title: Internationalisation (i18n)
description: Statidocs prend en charge nativement les sites multilingues.
---
# Internationalisation (i18n)

Statidocs prend en charge nativement les sites multilingues : localisation du contenu, traduction des templates (anglais et français inclus) et sélecteur de langue dans l’en-tête.

## Configurer l’i18n

Indiquez à Statidocs les langues prises en charge en les listant dans le fichier de configuration (`cecil.yml`) :

```yaml
language: en # default language
languages:
  - code: en
    name: English
    locale: en
  - code: fr
    enabled: true # disable with "false"
    name: Français
    locale: fr
```

Les options de configuration peuvent également être localisées, par langue :

```yaml
languages:
  - code: fr
    name: Français
    locale: fr
    config:
      baseline: Créez rapidement un site Web de documentation
```

## Traduire les pages

Dupliquez les pages à traduire en ajoutant le code de langue en suffixe, par exemple :

```text
<my-project>
└─ pages
   └─ docs
      ├─ index.md
      ├─ index.fr.md
      ├─ getting-started.md
      └─ getting-started.fr.md
```

La page traduite est disponible à l’adresse `/fr/docs/getting-started/`, et le sélecteur de langue pointe vers les traductions de la page courante.

:::tip
Consultez la [documentation multilingue de Cecil](https://cecil.app/documentation/content/#multilingual).
:::

## Traduire les groupes de la barre latérale

Le titre d’un groupe est traduit via les fichiers de traduction. Par exemple, pour un groupe `Reference`, ajoutez la ligne suivante dans `translations/messages.fr.yaml` :

```yaml
"Reference": "Référence"
```

Vous pouvez également traduire le fichier `index.md` du groupe (`index.fr.md`) pour localiser sa description et son contenu.

## Traduire les templates

Les libellés du thème (« Sur cette page », « Modifier cette page », etc.) sont déjà traduits en anglais et en français. Pour ajouter une langue ou surcharger un libellé, créez un fichier de traduction dans le répertoire `translations/` (par exemple `messages.de.yaml`).

:::tip
Consultez la [documentation de Cecil sur la localisation des templates](https://cecil.app/documentation/templates/#localization).
:::

## Mémoriser la langue choisie

L’option `language_cookie` enregistre la langue choisie avec le sélecteur dans un cookie, afin de rediriger les visiteurs vers leur langue. Par exemple, avec les [redirections de Netlify basées sur la langue](https://docs.netlify.com/routing/redirects/redirect-options/#redirect-by-country-or-language) :

```yaml
language_cookie: nf_lang
```
