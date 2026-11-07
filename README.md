# Wendy's Menu & Store Scraper [Just 💰$0.42]

Extract structured data from [wendys.com](https://wendys.com) — Wendy's (wendys.com) menus and restaurant details by address, ZIP code or restaurant ID: prices, calories, full nutrition, allergens, modifiers, hours and coordinates for every menu item. Structured rows for price tracking, nutrition datasets and spreadsheets.

**[Wendy's Menu & Store Scraper [Just 💰$0.42] on Apify →](https://apify.com/blackfalcondata/wendys-scraper?fpr=1h3gvi)**

---

## 🚀 How to use this actor

> ### 💚 $5 free Apify credits — every month
> No credit card required. No commitment. Cancel anytime.

### 👉 [Sign up free on Apify →](https://console.apify.com/sign-up?fpr=1h3gvi)

1. **Click sign up** — pick GitHub, Google, or email; takes ~30 seconds
2. **Open this actor** — input is pre-filled with a working example
3. **Click Start** — export results as JSON, CSV, or Excel

Your **$5 monthly platform credit** is enough to run this actor right away — and again every month — scraping typically several hundred to several thousand results per run, depending on your input.

## Key features

**Detail enrichment** — Fetch full descriptions, structured metadata for each product.

**Incremental mode** — Only get new or changed products since your last run. Content hash per product — no duplicates, no re-processing.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per ${NOUN} to control output size and cost.

**Result cap** — Stop after N products (up to 10.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every product returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured products from wendys.com on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor products, track trends, and analyze market dynamics with structured, deduplicated data from wendys.com.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired ${NOUNS}. Perfect for price-tracking, churn analysis, and alerting pipelines.

**AI / LLM training data**
Structured JSON per product is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "addresses": [
    "Birmingham, AL 35209"
  ],
  "country": "US",
  "maxResults": 150,
  "includeDetails": true,
  "descriptionMaxLength": 0,
  "compact": false,
  "excludeEmptyFields": false,
  "incrementalMode": false,
  "notifyOnlyChanges": false,
  "notificationLimit": 5,
  "descriptionFormat": "all"
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `addresses` | array | — | Where to look for restaurants: street addresses, cities, US/Canadian ZIP or postal codes, or "lat,lng" coordinates. Each entry finds the nearest restaurants. |
| `restaurantIds` | array | — | Wendy's restaurant numbers (for example 1252) to fetch directly, without an address search. |
| `maxStoresPerAddress` | integer | `1` | How many of the nearest restaurants to return for each address (1-50). Each restaurant adds its full menu to the output. |
| `searchRadiusMiles` | integer | `25` | How far from each address to look for restaurants (1-200 miles). |
| `categories` | array | — | Keep only menu items in these categories, for example Baconator or Frosty. Matching ignores upper and lower case. Leave empty for every category. |
| `includeModifiers` | boolean | `true` | Add each item's modifier groups and options (sizes, toppings, sides) to the record. Turn off for smaller records. |
| `country` | enum | `"US"` | Which market to search. |
| `maxResults` | integer | `150` | Maximum number of menu-item records to return (0 = unlimited). One restaurant's menu is roughly 150 records. |
| `includeDetails` | boolean | `true` | Refresh each restaurant's own profile (hours, amenities, coordinates) on top of the menu data. |
| `descriptionMaxLength` | integer | `0` | Truncate each item description to N characters. 0 = no truncation. |
| `compact` | boolean | `false` | Core fields only — item, category, price, calories, availability and store identity (for AI-agent/MCP workflows). |
| `excludeEmptyFields` | boolean | `false` | Drop null, empty-string, and empty-array fields from each record before push. Smaller payloads for AI agents and dashboards. |
| `incrementalMode` | boolean | `false` | Compare against the previous run and return only new or changed items (price, availability, description). stateKey is optional — it defaults to a value derived from your search inputs (addresses, restaurant IDs, country, categories) so different searches never share state. |
| `stateKey` | string | — | Optional. Stable identifier for the tracked search universe. Leave empty to auto-generate from search inputs. |
| `notifyOnlyChanges` | boolean | `false` | When Incremental Mode is on, only send notifications for NEW and UPDATED menu items. Has no effect outside incremental mode. |
| `notificationLimit` | integer | `5` | Maximum number of menu items included in each notification message (1–20). |
| `telegramToken` | string | — | Telegram bot token (from @BotFather). Required for Telegram notifications. |
| `telegramChatId` | string | — | Telegram chat or channel ID (e.g. "-100123456789"). Required when telegramToken is set. |
| `discordWebhookUrl` | string | — | Discord incoming webhook URL. Server Settings → Integrations → Webhooks → New Webhook. |
| `slackWebhookUrl` | string | — | Slack incoming webhook URL. api.slack.com/messaging/webhooks. |
| `whatsappPhoneNumberId` | string | — | Your WhatsApp Business phone-number ID (numeric, from Meta dashboard). Required when whatsappAccessToken is set. |
| `whatsappAccessToken` | string | — | WhatsApp Cloud API permanent access token (System User token from Meta Business). Recipient must have messaged the business number within the last 24h (service-conversation window — free since Nov 2024). |
| `whatsappTo` | string | — | Recipient phone in E.164 format without + (e.g. "436641234567"). Recipient must have messaged your business number within last 24h. |
| `webhookUrl` | string | — | Receives a JSON POST with {metadata, items} after each run. Universal escape hatch for n8n / Make / Zapier / custom backends. |
| `webhookHeaders` | object | — | Optional JSON object of custom headers (e.g. {"Authorization":"Bearer ..."}). |
| `appConnector` | string | — | Optional. Pick a connected app under Settings → API & Integrations to receive your results (including any contact details). Best-effort across MCP connectors as Apify expands its catalog. |
| `mcpIssueTeam` | string | — | Only when the connected app is an issue tracker: the team (name or ID) the summary issue is created under, if that app requires one. |
| `descriptionFormat` | enum | `"all"` | Choose which representation of the listing description to include. `all` keeps every variant; the others keep only the selected one. |
| `startUrls` | array | — | Wendy's ordering page URLs that contain a restaurant number, such as https://order.wendys.com/us/en/menu?siteNum=1252. When set, the address and restaurant ID fields are ignored. |

---

## Output fields

Every product returns the same 64-field schema. Missing values are `null` — never omitted.

- `listingId`
- `searchQuery`
- `contentQuality`
- `detailFetched`
- `source`
- `contentHash`
- `recordType`
- `type`
- `mode`
- `dedupeKey`
- `changeType`
- `scrapedAt`
- `sourceUrl`
- `portalUrl`
- `searchedAddress`
- `title`
- `entityName`
- `location`
- `restaurantId`
- `storeName`
- `storeAddress`
- `storeStreet`
- `storeCity`
- `storeState`
- `storePostalCode`
- `storeCountry`
- `storePhone`
- `latitude`
- `longitude`
- `storeLatitude`
- `storeLongitude`
- `distanceMiles`
- `hasBreakfast`
- `isOpen`
- `isOpen24Hours`
- `timezone`
- `hours`
- `storeAmenities`
- `itemName`
- `displayName`
- `itemId`
- `menuItemId`
- `salesItemId`
- `productId`
- `slug`
- `categoryId`
- `categoryName`
- `categoryNames`
- `price`
- `priceRange`
- `currency`
- `calories`
- `calorieRange`
- `nutrition`
- `allergens`
- `isAvailable`
- `isCombo`
- `isLimitedTimeOffer`
- `isFreestyle`
- `hasRequiredModifiers`
- `modifiers`
- `imageId`
- `description`
- `dayPart`

---

## Sample output

One object per product. Here is a real example from a production run:

```json
{
  "listingId": "3e526bca1d7616d9e412ee273d2bb1f2012f4fc4dae4c871a80020b486c4ba0b",
  "searchQuery": "Birmingham, AL 35209",
  "contentQuality": "full",
  "detailFetched": true,
  "source": "api.app.prd.wendys.digital",
  "contentHash": "8beb5db7e66b019f603cbdbc3e6ca83a1d0cd3c44531039365d4ef09d378c942",
  "recordType": "menuItem",
  "type": "menu-item",
  "mode": "storeSnapshot",
  "dedupeKey": "1252:30008",
  "changeType": "new",
  "scrapedAt": "2026-11-07T00:59:19.628Z"
}
```

*Truncated — full records contain 64 fields. See Output fields for the complete schema.*

**[Try Wendy's Menu & Store Scraper [Just 💰$0.42] now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/wendys-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.01 |
| Result | $0.000423 |

See the [actor on Apify](https://apify.com/blackfalcondata/wendys-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape wendys.com?**
Use this actor on Apify to extract structured data from wendys.com. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get wendys.com data as JSON, CSV, or Excel?**
The actor writes each product to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape wendys.com?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check wendys.com's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for ${NOUNS} extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each product gets a content hash. On subsequent runs, only new or changed products are emitted — saving time, compute, and storage. Expired products can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

[Browse all Black Falcon Data actors →](https://apify.com/blackfalcondata?fpr=1h3gvi)

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [Wendy's Menu & Store Scraper [Just 💰$0.42]](https://apify.com/blackfalcondata/wendys-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 11*
