---
title: Site Search
description: Add a search to Statidocs with the Algolia DocSearch or FlexSearch component theme.
---
# Site Search

Statidocs offers two search solutions, each one packaged as a dedicated [component theme](https://cecil.app/documentation/themes/) and displayed as a search button in the header:

- [Algolia DocSearch](#algolia-docsearch): a hosted search service, free for open-source projects;
- [FlexSearch](#flexsearch): a local search index, generated with your site, without any external service.

Both open a search modal with the `Ctrl`/`⌘` + `K` shortcut, support keyboard navigation, and are translated in English and French.

:::info
DocSearch takes precedence if both are installed and enabled.
:::

## Algolia DocSearch

The [DocSearch component theme](https://github.com/Cecilapp/theme-docsearch) queries an Algolia index of your website.

The service is free for any open-source project: [apply to the DocSearch program](https://docsearch.algolia.com/apply/). DocSearch crawls your website periodically and aggregates the content in an Algolia index, which is then queried directly from your front-end using the Algolia API.

:::info
If your website is [not eligible](https://docsearch.algolia.com/docs/who-can-apply/) for the free program or if it sits behind a firewall, you can [run your own](https://www.algolia.com/doc/tools/crawler/getting-started/overview/) crawler.
:::

### DocSearch installation

```bash
composer require cecil/theme-docsearch
```

Then add it after `docs` in the `theme` section of the configuration, with your Algolia credentials:

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
Use the **search-only** API key: it is published in the HTML of the pages.
:::

### DocSearch configuration

Main options (default values):

```yaml
docsearch:
  enabled: true # display the search box
  appId: '' # Algolia application ID
  indexName: '' # Algolia index name
  apiKey: '' # Algolia search API key
  language: true # filter the results on the current language (`lang` facet)
  insights: false # send search events to Algolia Insights
  debug: false # keep the modal open on blur
  placeholder: '' # placeholder of the search input
  search_parameters: {} # additional Algolia search parameters
```

See the [DocSearch component theme documentation](https://github.com/Cecilapp/theme-docsearch#configuration) for all options.

:::tip
Results are filtered on the current language, from the `docsearch:language` meta tag added to every page. Set `language: false` if your index has no `lang` facet.
:::

### Crawler configuration

When your website is accepted in the DocSearch program, Algolia creates a default crawler configuration, editable in the [Crawler dashboard](https://crawler.algolia.com).

With the Docs theme, the recommended record extractor is:

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

Declare `lang` in the `attributesForFaceting` of the index settings, to filter results by language:

```js
initialIndexSettings: {
  "<YOUR_INDEX_NAME>": {
    attributesForFaceting: ["type", "lang"],
    // ...
  },
},
```

See the [crawler configuration guide](https://github.com/Cecilapp/theme-docsearch/blob/main/docs/crawler.md) for a complete example.

## FlexSearch

As an alternative to DocSearch (no external service, no crawler), the [FlexSearch component theme](https://github.com/Cecilapp/theme-flexsearch) generates a search index at build time (a static JSON file per language), loaded on first use.

### FlexSearch installation

```bash
composer require cecil/theme-flexsearch
```

Then add it after `docs` in the `theme` section of the configuration:

```yaml
theme:
  - docs
  - flexsearch
```

:::tip
If DocSearch is also installed, disable it (`docsearch.enabled: false`) to use FlexSearch.
:::

### FlexSearch configuration

Results are grouped by section, in the order of `flexsearch.sections` (every root section is indexed by default):

```yaml
flexsearch:
  sections:
    docs:
      limit: 5 # maximum number of results in the group
```

Section options:

| Option   | Description                                                        | Default                   |
|----------|--------------------------------------------------------------------|---------------------------|
| `title`  | Title of the group of results.                                     | title of the section page |
| `limit`  | Maximum number of results displayed in the group.                  | `5`                       |
| `split`  | One record per `<h2>`/`<h3>` heading, or a single record per page. | `true`                    |
| `date`   | Display the page date in the results.                              | `false`                   |
| `length` | Maximum length of the indexed text of an unsplit page.             | `1000`                    |

Other options (default values):

```yaml
flexsearch:
  enabled: true # display the search box
  trigger: auto # trigger button: auto (icon only on mobile), icon or full
  hotkey: k # Ctrl/⌘ + hotkey opens the search box (false to disable)
  credit: true # display the "Search by FlexSearch" credit
  suggest: true # fall back to fuzzy matching when nothing matches strictly
```

See the [FlexSearch component theme documentation](https://github.com/Cecilapp/theme-flexsearch#configuration) for all options (tokenizer, encoder, fields weight, etc.).

:::info
Pages excluded from lists (`exclude: true`) are not indexed.
:::
