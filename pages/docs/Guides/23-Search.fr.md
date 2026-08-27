---
title: Recherche sur le site
description: Statidocs prend en charge Algolia DocSearch.
group: Guides
---
# Recherche sur le site

Statidocs prend en charge [Algolia DocSearch](https://docsearch.algolia.com).

Le service est gratuit pour tout projet open source : [inscrivez-vous au programme DocSearch](https://docsearch.algolia.com/apply/).

DocSearch explore votre site une fois par semaine et regroupe son contenu dans un index Algolia. Ce contenu est ensuite interrogé directement depuis votre interface avec l’API Algolia.

:::info
Si votre site n’est [pas éligible](https://docsearch.algolia.com/docs/who-can-apply/) à l’offre gratuite ou s’il se trouve derrière un pare-feu, vous pouvez [exécuter votre propre](https://docsearch.algolia.com/docs/run-your-own/) explorateur DocSearch.
:::

## Configuration de l’explorateur

La modification et la gestion de vos explorations s’effectuent via [l’interface web](https://crawler.algolia.com). Les index sont immédiatement disponibles après le déploiement ; une configuration manuelle n’est donc généralement pas nécessaire.

Configuration recommandée :

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
              selectors: "#sidebar ul>li>a.active",
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

## Configuration de DocSearch

```yaml
docsearch:
  enabled: true|false
  appId: <YOUR_APP_ID>
  indexName: <YOUR_INDEX_NAME>
  apiKey: <YOUR_SEARCH_API_KEY>
  insights: true|false
  debug: false|true
```
