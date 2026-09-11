# Google Ads Transparency Scraper — Apify Actor usage guide

From 1$/1000 results. Scrape Google Ads Transparency Center by advertiser URL. Get ad creatives, formats, targeting, regions, serving dates, headlines, CTAs and image URLs. Supports OCR text extraction, asset downloads, and bulk collection with maxResults. No API key needed.

> **This repository does not contain the Actor's source code.** The Actor
> itself is closed-source and runs on Apify's infrastructure — this repo is
> just documentation and example client code showing how to call it via the
> Apify API/SDK with your own Apify API token. Think of it as a "cookbook"
> repo, not the product itself.

**Run it on Apify →** [https://apify.com/leadsbrary/google-ads-transparency-scraper?fpr=aupara](https://apify.com/leadsbrary/google-ads-transparency-scraper?fpr=aupara)

## What it does

Automated scraper for the Google Ads Transparency Center that collects advertiser ad inventories and creative metadata at scale. The Actor uses a headless Chromium browser to navigate and paginate advertiser pages, intercepts Google Ads RPC responses to extract ad records, deduplicates creatives, optionally visits individual ad detail pages to harvest creative variations and targeting signals, and can run OCR on ad images and download media assets. Outputs are structured per-ad records containing ad links and identifiers, creative format and timing (first/last shown, days active), preview and asset URLs, OCR-extracted visible text (optional), creative variations (headlines, descriptions, CTAs, click and media URLs), per-region serving statistics, and targeting metadata (demographics, geography, contextual signals, advertiser lists).…

## Pricing

Pay-per-event pricing — you only pay for what the Actor actually delivers:

- **Actor Start** — $0.00005 (one-time, per run). Charged when the Actor starts running. Number of events charged depends on Actor memory (one event per GB, minimum one event).
- **result** — $0.0025–$0.001 depending on your Apify usage tier. Single result in the default dataset.

*(Apify may also charge a small amount for the platform compute the Actor
uses while running — see the [pricing tab](https://apify.com/leadsbrary/google-ads-transparency-scraper?fpr=aupara) on the Actor page
for exact current numbers.)*

## Quick start

You need an Apify account and API token (`console.apify.com` → Settings →
Integrations). Don't have one yet? See the signup section below — new
accounts get **$5 of free usage credit every month**.

### cURL

```bash
curl -X POST "https://api.apify.com/v2/acts/leadsbrary~google-ads-transparency-scraper/runs?token=YOUR_APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "startUrls": [
    {
      "url": "https://adstransparency.google.com/advertiser/AR08888592736429539329?authuser=0&region=ES&preset-date=Last+30+days"
    }
  ],
  "skipDetails": false,
  "shouldDownloadAssets": false,
  "shouldDownloadPreviews": false,
  "ocr": false,
  "maxResults": 1000
}'
```

### Python (`apify-client`)

```python
from apify_client import ApifyClient

client = ApifyClient("YOUR_APIFY_TOKEN")

run_input = {
  "startUrls": [
    {
      "url": "https://adstransparency.google.com/advertiser/AR08888592736429539329?authuser=0&region=ES&preset-date=Last+30+days"
    }
  ],
  "skipDetails": false,
  "shouldDownloadAssets": false,
  "shouldDownloadPreviews": false,
  "ocr": false,
  "maxResults": 1000
}

run = client.actor("leadsbrary/google-ads-transparency-scraper").call(run_input=run_input)

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

### JavaScript (`apify-client`)

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_APIFY_TOKEN' });

const runInput = {
  "startUrls": [
    {
      "url": "https://adstransparency.google.com/advertiser/AR08888592736429539329?authuser=0&region=ES&preset-date=Last+30+days"
    }
  ],
  "skipDetails": false,
  "shouldDownloadAssets": false,
  "shouldDownloadPreviews": false,
  "ocr": false,
  "maxResults": 1000
};

const run = await client.actor('leadsbrary/google-ads-transparency-scraper').call(runInput);
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

See [`example.py`](./example.py) in this repo for a complete runnable script.

## Don't have an Apify account yet?

[Sign up here](https://console.apify.com/sign-up?fpr=aupara) — new accounts get **$5 of free platform credit
every month**, enough to try most Actors without paying anything upfront.
Browsing for other tools? The full [Apify Store](https://apify.com/store?fpr=aupara) has thousands
of ready-made Actors.

## Links

- Actor page (run it, see live pricing/reviews): [https://apify.com/leadsbrary/google-ads-transparency-scraper?fpr=aupara](https://apify.com/leadsbrary/google-ads-transparency-scraper?fpr=aupara)
- All Actors from this developer: [https://apify.com/leadsbrary?fpr=aupara](https://apify.com/leadsbrary?fpr=aupara)
- Apify API docs: [https://docs.apify.com/api/v2](https://docs.apify.com/api/v2)

## License

The example code in this repository (README snippets, `example.py`) is
released under the MIT License — see [LICENSE](./LICENSE). This does not
cover the Actor itself, which remains closed-source and is operated by its
developer on the Apify platform.
