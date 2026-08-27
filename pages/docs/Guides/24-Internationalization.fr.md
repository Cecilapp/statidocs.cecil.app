---
title: Internationalisation (i18n)
description: Statidocs prend en charge nativement les sites multilingues.
group: Guides
---
# Internationalisation (i18n)

Statidocs prend en charge nativement les sites multilingues.

## Configurer l’i18n

Indiquez à Statidocs les langues prises en charge en renseignant les locales dans le fichier de configuration (`cecil.yml`) :

```yaml
language: en # langue par défaut
languages:
  - code: en
    name: English
    locale: en
  - code: fr
    enabled: true # désactiver avec "false"
    name: Français
    locale: fr
```

## Traduire les pages

Dupliquez les pages que vous souhaitez traduire en ajoutant le code de la langue comme suffixe, par exemple :

```text
<mon-projet>
└─ pages
   └─ docs
      ├─ getting-started.md
      └─ getting-started.fr.md
```

:::tip
[Documentation de Cecil](https://cecil.app/documentation/content/#multilingual)
:::

## Traduire les templates

:::tip
[Documentation de Cecil](https://cecil.app/documentation/templates/#localization)
:::
