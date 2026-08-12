# Grok Scraper

[![Grok Scraper by cloro](https://github.com/cloro-dev/grok-scraper/blob/main/grok-scraper-hero-image.png)](https://cloro.dev/grok/?utm_source=github)

[![cloro](https://img.shields.io/badge/Powered%20by-cloro-blue?style=for-the-badge)](https://cloro.dev/)

The [Grok scraper](https://cloro.dev/grok/?utm_source=github) by cloro returns Grok answers as structured JSON, with richer source metadata than the other AI surfaces: preview text, site name, author, favicon and image alongside the URL.

## How do you scrape Grok?

1. Get an API key at [cloro.dev](https://cloro.dev/?utm_source=github&utm_medium=readme).
2. POST a prompt to `https://api.cloro.dev/v1/monitor/grok`.
3. Read the parsed fields from the JSON response.

Grok's distinguishing feature for monitoring is recency. It leans on X for current events, so its citations move faster than the other engines and skew toward posts and news rather than evergreen pages. If you are tracking a launch or an incident, this is the surface where it shows up first.

### Request sample (Python)

```python
import requests

payload = {
    'prompt': 'what are people saying about the Google num=100 change',
    'country': 'US',
    'include': {'markdown': True},
}

response = requests.post(
    'https://api.cloro.dev/v1/monitor/grok',
    headers={'Authorization': 'Bearer YOUR_API_KEY'},
    json=payload,
)

print(response.json())
```

### Request sample (cURL)

```bash
curl -X POST https://api.cloro.dev/v1/monitor/grok \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"prompt": "latest news on AI search regulation", "country": "US"}'
```

Node.js and async/webhook examples are in the [endpoint documentation](https://cloro.dev/docs/api-reference/endpoint/monitor-grok).

### Request parameters

| Parameter | Description | Default |
| --- | --- | --- |
| `prompt`\* | The query or question (1-10,000 characters) | – |
| `country` | Country code for localized results (`US`, `GB`, `DE`) | `US` |
| `state` | US state code for finer localization | – |
| `include.markdown` | Return the answer as Markdown | `false` |
| `include.html` | Return a URL to the full HTML (expires after 24h) | `false` |
| `include.rawResponse` | Return the unparsed upstream payload | `false` |

\* Required

## What data does the Grok scraper return?

```json
{
  "success": true,
  "result": {
    "text": "Recent discussion centres on the removal of the num=100 parameter...",
    "sources": [
      {
        "position": 1,
        "url": "https://example.com/num100-analysis",
        "label": "Example Analysis",
        "description": "What the num=100 removal changed for rank tracking",
        "preview": "Google removed the num=100 parameter on September 11, 2025...",
        "siteName": "Example",
        "creator": "@example",
        "favicon": "https://example.com/favicon.ico",
        "image": "https://example.com/cover.png"
      }
    ],
    "markdown": "Recent discussion centres on..."
  }
}
```

Alongside `text` and `markdown`:

1. **`sources`** — with more metadata per entry than any other cloro surface: `preview`, `searchEngineText`, `siteName`, `metadataTitle`, `creator`, `image` and `favicon` on top of the usual position, URL, label and description.
2. **`citationPills`** — inline citation chips where present.
3. **`rawResponse`** — the unparsed upstream payload.

The `creator` field is why this surface is worth tracking separately: it names the account behind a cited post, which no other engine exposes.

Full field-level schemas are in the [endpoint reference](https://cloro.dev/docs/api-reference/endpoint/monitor-grok).

## Use cases

- **Real-time news and incident monitoring**, where Grok cites faster than the other engines.
- **Social listening with attribution** — `creator` names the account behind a cited post.
- **Launch tracking** — what the model says about a product in the days after announcement.
- **Cross-engine comparison** — Grok's source mix is the least like the others, so it is a useful outlier check.

## FAQ

### What makes Grok's sources different?

More metadata per source. Preview text, site name, author, favicon and image come back alongside the URL, so you can render a citation without a second fetch.

### Does Grok cite X posts?

Frequently, yes. That is the main reason its citation set diverges from Gemini or ChatGPT on the same prompt.

### Is scraping Grok allowed?

cloro reads publicly visible responses. Check your own jurisdiction and terms.

### What is the recommended timeout?

60 seconds.

## Learn more

- **Endpoint reference:** [cloro.dev/docs](https://cloro.dev/docs/api-reference/endpoint/monitor-grok)
- **Product page:** [cloro.dev/grok](https://cloro.dev/grok/)

## Other cloro scrapers

[AI Mode](https://cloro.dev/ai-mode/) · [AI Overview](https://cloro.dev/ai-overview/) · [ChatGPT](https://cloro.dev/chatgpt/) · [Copilot](https://cloro.dev/copilot/) · [Gemini](https://cloro.dev/gemini/) · [Google Search](https://cloro.dev/google-search/) · [Google News](https://cloro.dev/google-news/) · [Perplexity](https://cloro.dev/perplexity/)

## Contact us

Questions or support: [r/cloroapi](https://www.reddit.com/r/cloroapi/).
