<!--
URL: https://github.com/divyambhutani/crawl_core
Fetch date: 2026-08-18
Source type: community post
Research cluster: keyword-source-priority
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting previously-flagged thin coverage.
-->

# divyambhutani/crawl_core
URL: https://github.com/divyambhutani/crawl_core

A FastAPI service that takes a single URL, crawls the page, extracts HTML metadata, and classifies it into page type plus relevant topics.

- Stars: 0
- Forks: 0
- Watchers: 0
- Open issues: 0
- Default branch: main
- Created: 2026-05-04T08:36:22Z

## Languages

- Dockerfile
- Python

## Top Contributors

- divyambhutani (30 contributions)

---

## README

# crawl_core

A FastAPI service that crawls a URL, extracts metadata and body text, and classifies the page into a page type plus relevant topics. Handles both server-rendered and JS-heavy (SPA/CSR) pages using a hybrid fetch strategy.

## Features

- **Hybrid fetching**: fast `curl_cffi` with browser TLS fingerprinting (about 200ms), automatic Playwright fallback for JS-heavy pages
- **Anti-bot evasion**: browser-grade TLS impersonation, stealth Playwright contexts, Chrome 120 security headers
- **Rich metadata extraction**: title, description, canonical URL, Open Graph, Twitter Card, JSON-LD structured data, heading hierarchy
- **Clean body text**: trafilatura-based extraction with nav/footer/review stripping and site-specific pruning (e.g., Amazon review sections)
- **Page classification**: 22 page types, 32 IAB topic categories, keyword extraction, and one-line summaries
- **Dual classification backend**: local BART-MNLI zero-shot inference or cloud Gemini Flash via Vertex AI
- **Bearer token auth**: protects public deployments from abuse

## Architecture

```
POST /crawl { url }
  |
  |- 1. fetch(url)            -> HTML + resolved_url           curl_cffi, about 200ms
  |
  |- 2. analyze(html, url)    -> needs JS render?
  |      |- No                -> use HTML as-is
  |      |- Yes               -> Playwright fallback            about 3 to 8s
  |
  |- 3. parse(html)           -> metadata (OG, Twitter, JSON-LD, headings)
  |
  |- 4. extract(html)         -> clean body text + word count
  |
  |- 5. classify(text, ...)   -> page_type + topics + keywords + summary
  |      |- Local backend     -> BART-MNLI zero-shot + 4-tier keyword extraction
  |      |- Vertex backend    -> single Gemini Flash call (all-in-one)
  |
  |- 6. Return JSON
```

## Tech Stack

| Component | Choice | Why |
|-----------|--------|-----|
| HTTP client | curl_cffi | Browser-grade TLS fingerprint. `httpx` gets blocked by bot detection. |
| JS rendering | Playwright + stealth | Async API, resource blocking. Selenium is slower, no async. |
| HTML parsing | Selectolax (lexbor) | 10 to 30x faster than BS4. BS4+lxml fallback for edge cases. |
| Body extraction | trafilatura | Purpose-built for content extraction. Handles diverse layouts. |
| Keywords (local) | 4-tier hybrid | JSON-LD, then spaCy noun chunks, then OG tags, then YAKE statistical fallback |
| Classification (local) | BART-MNLI zero-shot | Any labels at runtime, no training data needed, runs locally. |
| Classification (cloud) | Gemini 2.5 Flash | Fast, cheap. Single call replaces BART plus keyword pipeline. |

## Quick Start

### Local (BART-MNLI backend)

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements-local.txt

# Download models
python -m spacy download en_core_web_sm
playwright install chromium

# Run
uvicorn app.main:app --host 0.0.0.0 --port 8000
```

### Cloud (Vertex AI backend)

```bash
# Set environment
export CLASSIFIER_BACKEND=vertex
export GOOGLE_CLOUD_PROJECT=your-project
export GOOGLE_CLOUD_LOCATION=us-central1
export API_TOKEN=your-secret-token

# Build and deploy
gcloud builds submit --tag us-central1-docker.pkg.dev/$GOOGLE_CLOUD_PROJECT/crawl-core/crawl-core:vertex
gcloud run deploy crawl-core \
  --image us-central1-docker.pkg.dev/$GOOGLE_CLOUD_PROJECT/crawl-core/crawl-core:vertex \
  --region us-central1 \
  --set-env-vars "CLASSIFIER_BACKEND=vertex,GOOGLE_CLOUD_PROJECT=$GOOGLE_CLOUD_PROJECT,GOOGLE_CLOUD_LOCATION=us-central1,API_TOKEN=$API_TOKEN" \
  --memory 2Gi --cpu 2 --timeout 300s \
  --min-instances 1 --max-instances 1 \
  --allow-unauthenticated
```

## API

### `POST /crawl`

```bash
curl -X POST http://localhost:8000/crawl \
  -H "Content-Type: application/json" \
  -d '{"url": "http://www.amazon.com/Cuisinart-CPT-122-Compact-2-Slice-Toaster/dp/B009GQ034C/ref=sr_1_1?s=kitchen&ie=UTF8&qid=1431620315&sr=1-1&keywords=toaster"}'
```

Response (excerpt):

```json
{
  "status": "success",
  "url": "http://www.amazon.com/Cuisinart-CPT-122-Compact-2-Slice-Toaster/dp/B009GQ034C/...",
  "render_method": "curl_cffi",
  "render_reason": "body has 1022685 chars and 101 content elements",
  "status_code": 200,
  "content_length": 2739582,
  "metadata": {
    "title": "Amazon.com: Cuisinart CPT-122 2-Slice Compact Plastic Toaster ...",
    "description": "Online Shopping for Kitchen Small Appliances ...",
    "canonical_url": "https://www.amazon.com/Cuisinart-CPT-122-2-Slice-Compact-Plastic/dp/B009GQ034C",
    "language": "en-us",
    "favicon": "https://www.amazon.com/favicon.ico",
    "open_graph": null,
    "twitter_card": null,
    "structured_data": [],
    "headings": {
      "h1": ["Cuisinart CPT-122 2-Slice Compact Plastic Toaster ...", "About this item", "Product information", "Product Summary: ..."],
      "h2": ["Frequently bought together", "Customers who viewed this item also viewed", "From the manufacturer", "..."]
    }
  },
  "content": {
    "body_text": "Cuisinart CPT-122 2-Slice Compact Plastic Toaster ... Purchase options and add-ons ... About this item ...",
    "word_count": 1055,
    "reading_time_minutes": 5.3
  },
  "classification": {
    "page_type": "product listing",
    "page_type_confidence": 0.334,
    "topics": [
      { "topic": "Shopping", "relevance_score": 0.992 },
      { "topic": "Home", "relevance_score": 0.989 },
      { "topic": "Food", "relevance_score": 0.955 }
    ],
    "iab_categories": ["Shopping", "Home", "Food"],
    "keywords": [
      "Amazon.com", "Cuisinart CPT-122", "2-Slice Compact Plastic Toaster", "Slots",
      "Bagels", "Bread", "7 Shade Settings", "Cancel/Defrost/Reheat Functions",
      "Removable Crumb Tray", "Small Kitchen Appliance"
    ],
    "summary": "Amazon.com: Cuisinart CPT-122 2-Slice Compact Plastic Toaster, a product listing about Shopping, Home, Food."
  },
  "error": null
}
```

## Local vs. Cloud tradeoffs

| | Local (BART-MNLI) | Cloud (Vertex AI Gemini) |
|---|---|---|
| **Image size** | about 4 GB (includes torch) | about 1.5 GB |
| **RAM at runtime** | about 3 GB (model weights) | about 512 MB |
| **Classification** | Two NLI passes (page type + topics) | Single Gemini API call |
| **Keywords** | 4-tier hybrid extraction | Gemini extracts inline |
| **Summary** | Template-based from structured data | Gemini generates |
| **Latency** | about 800ms (GPU) / about 5s+ (CPU) | about 1 to 2s |
| **Cost** | Free (local compute) | about $0.001/request |
| **Dependencies** | torch, transformers, spacy, yake | google-genai |
