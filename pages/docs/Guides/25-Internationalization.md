---
title: Internationalization (i18n)
description: Statidocs provides built-in support for multilingual sites.
---
# Internationalization (i18n)

Statidocs provides built-in support for multilingual sites: content localization, templates translation (English and French included) and a language selector in the header.

## Configure i18n

Tell Statidocs about the languages you support by listing them in the configuration (`cecil.yml`) file:

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

Configuration options can also be localized, per language:

```yaml
languages:
  - code: fr
    name: Français
    locale: fr
    config:
      baseline: Créez rapidement un site Web de documentation
```

## Translate pages

Duplicate pages you want to translate by adding the language code as suffix, for example:

```text
<my-project>
└─ pages
   └─ docs
      ├─ index.md
      ├─ index.fr.md
      ├─ getting-started.md
      └─ getting-started.fr.md
```

The translated page is available at `/fr/docs/getting-started/`, and the language selector links the translations of the current page.

:::tip
See the [Cecil multilingual documentation](https://cecil.app/documentation/content/#multilingual).
:::

## Translate sidebar groups

The title of a group is translated through the translations files. For example, with a `Reference` group, add the following line to `translations/messages.fr.yaml`:

```yaml
"Reference": "Référence"
```

You can also translate the `index.md` file of the group (`index.fr.md`) to localize its description and content.

## Translate templates

The labels of the theme (“On this page”, “Edit this page”, etc.) are already translated in English and French. To add a language or override a label, create a translation file in the `translations/` directory (e.g. `messages.de.yaml`).

:::tip
See the [Cecil templates localization documentation](https://cecil.app/documentation/templates/#localization).
:::

## Remember the chosen language

The `language_cookie` option stores the language chosen with the selector in a cookie, to redirect visitors to their language. For example, with [Netlify redirects based on language](https://docs.netlify.com/routing/redirects/redirect-options/#redirect-by-country-or-language):

```yaml
language_cookie: nf_lang
```
