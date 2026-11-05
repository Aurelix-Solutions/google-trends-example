# Google Trends Scraper: Python example

A small, runnable example for [Google Trends Scraper](https://apify.com/aurelix/google-trends-scraper), an Apify Actor by Aurelix.

## What it does

Google Trends Scraper turns Google Trends into clean rows: for every keyword you get the interest-over-time timeline with average, peak and latest value, interest by country, state, metro area or city, and top and rising related queries with growth such as +250% or Breakout. Type keywords or paste Google Trends explore links (the terms, location, time range, category and search type are read from each link). Give hundreds of keywords at once: they are compared 5 at a time with a shared anchor keyword, so every value sits on one 0-100 scale. Choose any time range, category and search type (web, YouTube, News, Images, Shopping), and add Google's Trending now searches for any country.

## Why this over alternatives

Compared with the leading alternatives on the Apify Store (the same table is on the Store page):

| | **This Actor** | apify/google-trends-scraper | data_xplorer/google-trends-fast-scraper |
|---|---|---|---|
| **Price per 1,000 results, free plan** | $1.50 | $3.00 | $2.00 |
| **Price per 1,000 results, paid plans** | $0.90 | $1.00 | $1.00 |
| **Start fee per run** | $0.0075 | $0 | $0.025 |
| **Platform usage billed on top** | No | Yes (4 GB default memory) | No |
| **Google Trends URL input** | ✓ | ✓ | ✗ |
| **Keywords per run** | Any number, one 0-100 scale | List of search terms | 1 |
| **Interest by region** | ✓ country, state, metro, city | ✓ subregion, city | ✓ |
| **Related queries** | ✓ top and rising, Breakout flag | ✓ top and rising | ✓ |
| **Trending searches by country** | ✓ | ✗ | ✓ |
| **YouTube, News, Images, Shopping search** | ✓ | not stated | ✗ |

- Runs finish: blocked keyword groups are retried, then named in the status, never a crashed run.
- Paste Google Trends explore URLs: terms, location, dates, category and search type are read from each link.
- Built for reliability: backoff and a fresh session on every rate limit, residential proxy only when needed.
- Hundreds of keywords per run, all on one comparable 0-100 scale through a shared anchor keyword.
- One clean record per keyword: timeline, regions, related queries, plus average, peak and latest value.
- Region level of your choice: country, state or province, US metro area, or city with coordinates.
- Rising queries flag Breakout terms, the fastest-growing searches Google reports.
- Trending now searches per country with search volume, growth, start time and topics.

## When to use it

- SEO and content teams ranking hundreds of keyword ideas by real search interest
- E-commerce and product teams spotting seasonal peaks and rising product searches
- Market researchers comparing brands or products across states, metro areas and cities
- Newsrooms and social teams monitoring what is trending now in each country
- Analysts and data scientists feeding search-interest series into dashboards and models

## Input example

This is the `google-trends-keyword-comparison` input used in `main.py`:

```json
{
  "keywords": [
    "iphone",
    "samsung galaxy",
    "google pixel"
  ],
  "geo": "US",
  "timeRange": "today 12-m"
}
```

Every input field is documented on the [Store page](https://apify.com/aurelix/google-trends-scraper).

## How to run

1. Get an Apify API token from Apify Console (Settings, API & Integrations).
2. Install and run:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
export APIFY_TOKEN=your_token_here
python main.py
```

The script starts a run of `aurelix/google-trends-scraper`, prints a few fields from the first results and writes every result to `results.csv`. Lists and nested objects are stored in the CSV as JSON text. Each run is billed to your Apify account (see Pricing below).

## Sample output

One record as returned by a real run (long text is shortened):

```json
{
  "record_type": "keyword",
  "keyword": "pickleball",
  "geo": "US",
  "time_range": "today 12-m",
  "category": 0,
  "property": "web",
  "compared_with": [
    "air fryer",
    "solar panels"
  ],
  "anchor_keyword": "air fryer",
  "on_shared_scale": true,
  "average_interest": 25.49,
  "peak_interest": 40,
  "peak_time": "2026-04-12T00:00:00Z",
  "latest_interest": 17,
  "top_related_query": "pickleball paddle",
  "top_rising_query": "charlie kirk mentor pickleball",
  "top_region": "Wyoming",
  "interest_over_time": [
    {
      "time": "2025-11-02T00:00:00Z",
      "value": 22,
      "is_partial": false
    },
    {
      "time": "2025-11-09T00:00:00Z",
      "value": 22,
      "is_partial": false
    },
    {
      "time": "2025-11-16T00:00:00Z",
      "value": 21,
      "is_partial": false
    },
    "... [50 more]"
  ],
  "interest_by_region": [
    {
      "geo_code": "US-WY",
      "geo_name": "Wyoming",
      "value": 100
    },
    {
      "geo_code": "US-UT",
      "geo_name": "Utah",
      "value": 68
    },
    {
      "geo_code": "US-HI",
      "geo_name": "Hawaii",
      "value": 66
    },
    "... [48 more]"
  ],
  "region_resolution": "REGION",
  "related_queries_top": [
    {
      "query": "pickleball paddle",
      "value": 100,
      "link": "https://trends.google.com/trends/explore?q=pickleball+paddle&date=today+12-m&geo=US"
    },
    {
      "query": "pickleball courts",
      "value": 49,
      "link": "https://trends.google.com/trends/explore?q=pickleball+courts&date=today+12-m&geo=US"
    },
    {
      "query": "pickleball near me",
      "value": 37,
      "link": "https://trends.google.com/trends/explore?q=pickleball+near+me&date=today+12-m&geo=US"
    },
    "... [22 more]"
  ],
  "related_queries_rising": [
    {
      "query": "charlie kirk mentor pickleball",
      "value": 3800,
      "growth": "+3,800%",
      "is_breakout": false,
      "link": "https://trends.google.com/trends/explore?q=charlie+kirk+mentor+pickleball&date=today+12-m&geo=US"
    },
    {
      "query": "jeff webb pickleball accident",
      "value": 3500,
      "growth": "+3,500%",
      "is_breakout": false,
      "link": "https://trends.google.com/trends/explore?q=jeff+webb+pickleball+accident&date=today+12-m&geo=US"
    },
    {
      "query": "best pickleball paddles 2026",
      "value": 3150,
      "growth": "+3,150%",
      "is_breakout": false,
      "link": "https://trends.google.com/trends/explore?q=best+pickleball+paddles+2026&date=today+12-m&geo=US"
    },
    "... [22 more]"
  ],
  "related_topics_top": [],
  "related_topics_rising": [],
  "trends_url": "https://trends.google.com/trends/explore?date=today%2012-m&q=pickleball&geo=US",
  "source_url": "https://trends.google.com/trends/api/explore?hl=en-US&tz=0&req=%7B%22comparisonItem%22%3A%5B%7B%22keyword%22%3A%22air%20fryer%22%2C%22geo%22%3A%22US%22%2C%22time%22%3A%22today%2012-m%22%7D%2C%7B%22keyword%22%3A%22pickleball%22%2C%22geo%22%3A%22US%22%2C%22time%22%3A%22today%2012-m%22%7D%2C%7B%22keywo... [141 more characters]",
  "scraped_at": "2026-11-04T19:28:07Z"
}
```

## Export to CSV

`main.py` writes `results.csv` with the `csv` module. You can also download any run's results directly:

```
https://api.apify.com/v2/datasets/<datasetId>/items?format=csv&clean=true
```

Send your token in an `Authorization: Bearer <token>` header (or `?token=`) if the dataset is not readable without one. Other formats: `format=json`, `format=xlsx`.

## Google Sheets

- Simplest: use Apify's Google Sheets integration on the Actor or a saved task, so each run's results land in a sheet with no token in the sheet itself.
- Quick pull of one run: `=IMPORTDATA("https://api.apify.com/v2/datasets/<datasetId>/items?format=csv&clean=true")`. This only works without a token if your account lets anyone with the dataset ID read it. Do not paste an API token into a sheet formula: anyone who can view or copy the sheet can read it and use your account.

## n8n

- Apify node: choose "Run an Actor", enter `aurelix/google-trends-scraper`, paste the input above, then read the run's dataset items.
- HTTP Request node: `POST https://api.apify.com/v2/acts/aurelix~google-trends-scraper/run-sync-get-dataset-items` with header `Authorization: Bearer <token>` (stored as an n8n credential) and the input as the JSON body. The response is the list of results. This endpoint waits for the run to finish, so for large runs start the run asynchronously and fetch the dataset when it ends.

## Limits

- Google Trends values are relative (0-100), not absolute search counts; trending searches give Google's approximate volume such as 200000.
- Related topics: Google currently returns empty topic lists to automated visitors (we tested plain requests and a real browser); the option is kept and costs nothing extra, but expect empty lists.
- Google samples its data, so the same request can differ by a few points between runs; rising related queries vary more, since Google samples them per request and per network.
- Keywords with very low search volume return no data; they are named in the run status and not charged.
- On one shared scale, keywords far smaller than the largest one can round to 0; run them separately or with a smaller first keyword.
- Large runs take time: about 2 to 3 Google requests per keyword at a polite pace; results are saved if the run nears its timeout.
- If Google keeps refusing a comparison group after every retry, its keywords are named in the run status and not charged.
- Google Trends URLs: only explore links are read (not Trending now or Year in Search pages), and their date must be one of the preset ranges or 'YYYY-MM-DD YYYY-MM-DD'.

## Pricing

At the time of writing:

Pay per event: you pay only for what the run returns, plus a small start fee.

| Event | Free plan | Paid plans (Bronze, Silver, Gold) |
|---|---|---|
| `trends-result` | $1.50 per 1,000 results | $0.90 per 1,000 results |
| `apify-actor-start` | $0.0075 per run | $0.0075 per run |

A result is one keyword's whole record (timeline, regions and related queries together) or one trending search. Keywords Google has no data for are not charged. The run start fee is $0.0075; it covers runs that return nothing.

Check the [Store page](https://apify.com/aurelix/google-trends-scraper) for current prices.

## Links

- Actor: https://apify.com/aurelix/google-trends-scraper
- Questions, bugs and feature requests: the Issues tab on the Store page.

## Licence

The example code in this repository is released under the MIT licence (see `LICENSE`). The Actor itself runs on Apify and is billed through your Apify account.
