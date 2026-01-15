# Grok scraper

[![Grok scraper by cloro](https://github.com/cloro-dev/grok-scraper/blob/main/grok-scraper-hero-image.png)](https://cloro.dev/grok/?utm_source=github)

[![cloro](https://img.shields.io/badge/Powered%20by-cloro-blue?style=for-the-badge)](https://cloro.dev/)

The [Grok Scraper](https://cloro.dev/grok/) by cloro enables developers to programmatically interact with Grok and automatically collect AI-powered search responses along with structured metadata. Instead of manual data collection, you can retrieve results as parsed JSON, raw HTML, or other formats for seamless integration into your workflows.

You can use cloro's Grok Scraper for current events monitoring, news tracking, research automation, and competitive analysis. It handles dynamic AI-generated content, supports real-time extraction, and eliminates the need to manage authentication, sessions, or anti-bot systems.

## How it works

The Grok scraper handles the rendering, parsing, and delivery of results in your requested format. You provide your search query, API credentials, and optional parameters as shown below.

### Request sample (Python)

```python
import json
import requests

# API parameters
payload = {
    'prompt': 'What are the latest developments in quantum computing 2025?',
    'country': 'US',
    'include': {
        'markdown': True
    }
}

# Get a response
response = requests.post(
    'https://api.cloro.dev/v1/monitor/grok',
    headers={'Authorization': 'Bearer YOUR_API_KEY'},
    json=payload
)

# Print response to stdout
print(response.json())

# Save response to a JSON file
with open('response.json', 'w') as file:
    json.dump(response.json(), file, indent=2)
```

### Request sample (cURL)

```bash
curl -X POST https://api.cloro.dev/v1/monitor/grok \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "What are the latest developments in quantum computing 2025?",
    "country": "US",
    "include": {
      "markdown": true
    }
  }'
```

### Request sample (Node.js)

```javascript
const axios = require("axios");

const payload = {
  prompt: "What are the latest developments in quantum computing 2025?",
  country: "US",
  include: {
    markdown: true,
  },
};

axios
  .post("https://api.cloro.dev/v1/monitor/grok", payload, {
    headers: {
      Authorization: "Bearer YOUR_API_KEY",
      "Content-Type": "application/json",
    },
  })
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

### Request parameters

| Parameter          | Description                                                                 | Default value |
| ------------------ | --------------------------------------------------------------------------- | ------------- |
| `prompt`\*         | The search query or question to ask Grok (1-10,000 characters)              | –             |
| `country`          | Optional country/region code for localized results (e.g., `US`, `GB`, `DE`) | `US`          |
| `include.markdown` | Include response in Markdown format when set to true                        | `false`       |
| `include.html`     | Include URL to full HTML response when set to true (URL expires after 24h)  | `false`       |

\* Mandatory parameters

---

### Output samples

The Grok Scraper API returns a structured JSON object containing Grok's AI-generated response and metadata with enhanced source information.

**Structured JSON output snippet:**

```json
{
  "success": true,
  "result": {
    "text": "Recent developments in quantum computing include breakthrough error correction methods, increased qubit stability, and practical applications in cryptography...",
    "sources": [
      {
        "position": 1,
        "url": "https://example.com/quantum-breakthrough",
        "label": "MIT Technology Review",
        "description": "Scientists achieve 99.9% qubit fidelity in room temperature conditions...",
        "preview": "When looking for a programming laptop, prioritize RAM and processor power...",
        "searchEngineText": "Top Development Laptops 2025",
        "siteName": "TechCrunch",
        "metadataTitle": "Ultimate Guide to Programming Laptops",
        "creator": "Tech Team",
        "image": "https://techcrunch.com/preview.jpg",
        "favicon": "https://techcrunch.com/favicon.ico"
      }
    ],
    "html": "https://storage.cloro.dev/results/c45a5081-808d-4ed3-9c86-e4baf16c8ab8/page-1.html", // URL expires after 24 hours
    "markdown": "**Recent developments in quantum computing** include breakthrough error correction methods..."
  }
}
```

## Enhanced source metadata

Grok provides comprehensive metadata for each source, going beyond basic link information to include rich contextual data:

| Field              | Type    | Description                                   |
| ------------------ | ------- | --------------------------------------------- |
| `position`         | integer | Position order of the source in the response  |
| `url`              | string  | Direct URL to the source content              |
| `label`            | string  | Source name or publication                    |
| `description`      | string  | Brief description of what the source contains |
| `preview`          | string  | Text snippet preview from the source          |
| `searchEngineText` | string  | Search engine display text for the source     |
| `siteName`         | string  | Website name                                  |
| `metadataTitle`    | string  | Source page metadata title                    |
| `creator`          | string  | Content creator or author                     |
| `image`            | string  | URL to preview image from the source          |
| `favicon`          | string  | URL to website favicon                        |

This enhanced metadata enables deeper analysis and better understanding of source context, attribution, and credibility.

### Real-time web sources

Grok integrates with real-time web sources, providing current and up-to-date information with detailed metadata for each source. The enhanced source structure includes preview text, search engine display text, site information, creator details, and image URLs for comprehensive context.

## Practical Grok scraper use cases

1. **Real-time news monitoring:** Track breaking news and current events with enhanced source attribution and preview capabilities.
2. **Research automation:** Gather comprehensive information with detailed source metadata including creator information and site context.
3. **Content verification:** Fact-check information using Grok's enhanced source attribution with preview text and metadata.
4. **Market intelligence:** Monitor industry trends and competitive landscape with rich source metadata for deeper analysis.
5. **Social media analysis:** Track trending topics and viral content with detailed source information including creator and site details.
6. **Brand monitoring:** Monitor brand mentions and sentiment across real-time web sources with enhanced attribution.
7. **Academic research:** Collect comprehensive data with detailed source citations including author information and metadata.
8. **SEO analysis:** Analyze search result patterns and source attribution with enhanced metadata for search engine optimization insights.

## Why choose cloro?

- **Simple integration:** Clean API design with comprehensive documentation and examples.
- **Reliable performance:** >99% uptime and low latencies (P50 < 30s, P90 < 60s)
- **No infrastructure hassle:** We handle rate limiting and browser management.
- **Real-time data:** Access to current information with enhanced source attribution.
- **Developer support:** Responsive support team to help with integration and troubleshooting.
- **Enhanced metadata:** Rich source information including preview text, creator details, and site context.

## FAQ

### Is scraping Grok allowed?

Any website is legal to be scraped as long as the information is publicly accessible.

### What makes cloro's Grok scraper unique?

cloro's Grok endpoint provides reliable access to Grok's AI-powered search with:

- **Enhanced source metadata** including preview text, search engine display text, site information, creator details, and image URLs
- **Real-time web source integration** for current information and breaking news
- **Comprehensive structured data extraction** for seamless integration into your workflows
- **Multi-format responses** including text, HTML, markdown, and rich structured objects
- **Detailed attribution** with creator information and site context for better source verification

### What's the recommended timeout for requests?

We don't recommend putting any timeout, given that our system retries automatically. We recommend setting up a retry mechanism in case of failure.

### How current is the information from Grok?

Grok provides real-time access to current information and breaking news through its web integration, making it ideal for monitoring current events and recent developments in any field.

### Does the API support different countries?

Yes, you can specify country codes like `US`, `GB`, `DE`, `JP`, `IN`, `BR` and more to get localized results and sources relevant to specific regions.

### What's the difference between Grok and other AI search scrapers?

Grok provides enhanced source metadata that goes beyond basic link information. Each source includes preview text, search engine display text, site name, metadata title, creator information, and image URLs. This richer context enables deeper analysis and better understanding of source credibility and attribution.

## Learn more

For detailed documentation, advanced features, and integration guides, visit:

- **API documentation:** [docs.cloro.dev](https://docs.cloro.dev)
- **Grok scraper page:** [cloro.dev/grok](https://cloro.dev/grok/)

## Other available scrapers

- **[AI Mode](https://cloro.dev/ai-mode/)** - Extracts structured data from Google AI Mode for general knowledge queries, workflow optimization, and technical guidance.
- **[AI Overview](https://cloro.dev/ai-overview/)** - Extracts structured data from Google AI Overview for comprehensive search result analysis and AI-curated insights.
- **[ChatGPT](https://cloro.dev/chatgpt/)** - Extracts structured data from ChatGPT with advanced features including shopping cards, raw response data, and query fan-out.
- **[Copilot](https://cloro.dev/copilot/)** - Extracts structured data from Microsoft Copilot for development tools, Microsoft ecosystem research, and enterprise-focused queries.
- **[Gemini](https://cloro.dev/gemini/)** - Extracts structured data from Google Gemini for complex reasoning, content generation, and source confidence scoring.
- **[Google](https://cloro.dev/google-search/)** - Extracts structured data from Google Search results, including organic results, People Also Ask questions, related searches, and optional AI Overview data.
- **[Grok](https://cloro.dev/grok/)** - Extracts comprehensive structured data from Grok with real-time web sources and enhanced source metadata for deeper analysis.
- **[Perplexity](https://cloro.dev/perplexity/)** - Extracts comprehensive structured data from Perplexity AI with real-time web sources, automatically detecting and extracting rich data objects.

## Contact us

If you have questions or need support, reach out to us on [our contact page](https://cloro.dev/contact).

---

Built with ❤️ by the cloro team
