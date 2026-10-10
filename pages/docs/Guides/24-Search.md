---
title: Site Search
description: Statidocs has support for Algolia DocSearch and FlexSearch.
---
# Site Search

Statidocs offers two search solutions, displayed as a search button in the header:

- [Algolia DocSearch](#algolia-docsearch): a hosted search service, free for open-source projects;
- [FlexSearch](#flexsearch): a local search index, generated with your site, without any external service.

:::info
DocSearch takes precedence if both are enabled.
:::

## Algolia DocSearch

The service is free for any open-source project: [apply to the DocSearch program](https://docsearch.algolia.com/apply/).

DocSearch crawls your website once a week and aggregates the content in an Algolia index. This content is then queried directly from your front-end using the Algolia API.

:::info
If your website is [not eligible](https://docsearch.algolia.com/docs/who-can-apply/) for the free or if your website sits behind a firewall, then you can [run your own](https://docsearch.algolia.com/docs/run-your-own/) DocSearch crawler.
:::

### Crawler configuration

Editing and managing your crawls can be done via [the web interface](https://crawler.algolia.com). Indices are readily available after deployment, so manual configuration usually isn't necessary.

Recommended configuration:

```json
new Crawler({
  appId: "YOUR_APP_ID",
  apiKey: "YOUR_SEARCH_API_KEY",
  indexPrefix: "",
  rateLimit: 8,
  maxDepth: 10,
  maxUrls: 5000,
  startUrls: ["https://YOUR_WEBSITE_URL"],
  renderJavaScript: false,
  sitemaps: ["https://YOUR_WEBSITE_URL/sitemap.xml"],
  ignoreCanonicalTo: false,
  discoveryPatterns: ["https://YOUR_WEBSITE_URL/**"],
  actions: [
    {
      indexName: "YOUR_INDEX_NAME",
      pathsToMatch: ["https://YOUR_WEBSITE_URL/**"],
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
    },
  ],
  safetyChecks: { beforeIndexPublishing: { maxLostRecordsPercentage: 30 } },
  initialIndexSettings: {
    staticecil: {
      attributesForFaceting: ["type", "lang"],
      attributesToRetrieve: [
        "hierarchy",
        "content",
        "anchor",
        "url",
        "url_without_anchor",
        "type",
      ],
      attributesToHighlight: ["hierarchy", "content"],
      attributesToSnippet: ["content:10"],
      camelCaseAttributes: ["hierarchy", "content"],
      searchableAttributes: [
        "unordered(hierarchy.lvl0)",
        "unordered(hierarchy.lvl1)",
        "unordered(hierarchy.lvl2)",
        "unordered(hierarchy.lvl3)",
        "unordered(hierarchy.lvl4)",
        "unordered(hierarchy.lvl5)",
        "unordered(hierarchy.lvl6)",
        "content",
      ],
      distinct: true,
      attributeForDistinct: "url",
      customRanking: [
        "desc(weight.pageRank)",
        "desc(weight.level)",
        "asc(weight.position)",
      ],
      ranking: [
        "words",
        "filters",
        "typo",
        "attribute",
        "proximity",
        "exact",
        "custom",
      ],
      highlightPreTag: '<span class="algolia-docsearch-suggestion--highlight">',
      highlightPostTag: "</span>",
      minWordSizefor1Typo: 3,
      minWordSizefor2Typos: 7,
      allowTyposOnNumericTokens: false,
      minProximity: 1,
      ignorePlurals: true,
      advancedSyntax: true,
      attributeCriteriaComputedByMinProximity: true,
      removeWordsIfNoResults: "allOptional",
    },
  },
});
```

### DocSearch configuration

```yaml
docsearch:
  enabled: true|false
  appId: <YOUR_APP_ID>
  indexName: <YOUR_INDEX_NAME>
  apiKey: <YOUR_SEARCH_API_KEY>
  insights: true|false
  debug: false|true
```

## FlexSearch

As an alternative to DocSearch (no external service, no crawler), install the [FlexSearch component theme](https://github.com/Cecilapp/theme-flexsearch):

```bash
composer require cecil/theme-flexsearch
```

Then add it after `docs` in the `theme` section of the configuration:

```yaml
theme:
  - docs
  - flexsearch
```

The search index is generated at build time, and results can be grouped by section:

```yaml
flexsearch:
  sections:
    docs:
      limit: 5
```

:::tip
Don’t forget to disable DocSearch (`docsearch.enabled: false`) to use FlexSearch.
:::
