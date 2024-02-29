# Site Search

Statidocs has support for [Algolia DocSearch](https://docsearch.algolia.com/).

The service is free for any open-source project: [apply to the DocSearch program](https://docsearch.algolia.com/apply).

DocSearch crawls your website once a week and aggregates the content in an Algolia index. This content is then queried directly from your front-end using the Algolia API.

:::info
If your website is [not eligible](https://docsearch.algolia.com/docs/who-can-apply) for the free or if your website sits behind a firewall, then you can [run your own](https://docsearch.algolia.com/docs/run-your-own/) DocSearch crawler.
:::

## Configuration

```yaml
docsearch:
  enabled: true|false
  appId: <YOUR_APP_ID>
  indexName: <YOUR_INDEX_NAME>
  apiKey: <YOUR_SEARCH_API_KEY>
  debug: false|true
```