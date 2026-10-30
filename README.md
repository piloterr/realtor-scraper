<p align="center">
  <a href="https://www.piloterr.com"><img src="images/banner.png" alt="Realtor.com Scraper API by Piloterr – scrape Realtor.com data as JSON" width="100%"></a>
</p>

# Realtor.com Scraper API

[![Discord](https://img.shields.io/badge/Discord-Join%20the%20community-5865F2?logo=discord&logoColor=white)](https://discord.gg/CFj3ph8aHU) [![Get API key](https://img.shields.io/badge/Piloterr-Get%20a%20free%20API%20key-111827)](https://app.piloterr.com) [![API docs](https://img.shields.io/badge/Docs-OpenAPI-0EA5E9)](https://app.piloterr.com/openapi) [![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

The **Piloterr Realtor.com Scraper API** lets you extract public data from Realtor.com as **clean, structured JSON** — no proxies, headless browsers or HTML parsing to maintain. Endpoints available in production:

- **Realtor Property API** — Extract full property details from a Realtor.com listing URL, including price, specs, photos, agents, features, and location data.
- **Realtor Search API** — Search Realtor.com listings from a search URL and retrieve prices, beds, baths, sqft, photos, and property metadata.

Use it for property price monitoring, market analytics, investment sourcing or rental yield models.

| Endpoint | Path | Credits | What you get |
|---|---|---|---|
| [Realtor Property API](#realtor-property-api) | `/v2/realtor/property` | 2 | Extract full property details from a Realtor.com listing URL, including price, specs, photos, agents, features, and location data. |
| [Realtor Search API](#realtor-search-api) | `/v2/realtor/search` | 2 | Search Realtor.com listings from a search URL and retrieve prices, beds, baths, sqft, photos, and property metadata. |

## Table of contents

- [How it works](#how-it-works)
- [Realtor Property API](#realtor-property-api)
- [Realtor Search API](#realtor-search-api)
- [Code examples in other languages](#code-examples-in-other-languages)
- [Practical use cases](#practical-use-cases)
- [Why Piloterr?](#why-piloterr)
- [FAQ](#faq)
- [Related scrapers](#related-scrapers)
- [Support](#support)

## How it works

1. **Create a free Piloterr account** and copy your API key from the [dashboard](https://app.piloterr.com).
2. **Send a `GET` (or `POST`) request** to `https://api.piloterr.com/v2/...` with the header `x-api-key: YOUR_API_KEY`.
3. **Receive structured JSON** — Piloterr handles rendering, proxies, retries and parsing.

```bash
export PILOTERR_API_KEY="your-api-key"
pip install requests        # Python
# TypeScript: Node.js 18+ (native fetch), run with `npx tsx file.ts`
```

> Every endpoint accepts both `GET` (query string) and `POST` (JSON body with the same fields).

## Realtor Property API

Extract full property details from a Realtor.com listing URL, including price, specs, photos, agents, features, and location data.

`GET | POST https://api.piloterr.com/v2/realtor/property` · **2 credits per request** · [Full reference](https://app.piloterr.com/openapi)

### Request parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `query` | string | ✅ | Full Realtor.com property detail URL. |

### Python example

```python
import json
import os
import requests

response = requests.get(
    "https://api.piloterr.com/v2/realtor/property",
    headers={"x-api-key": os.environ["PILOTERR_API_KEY"]},
    params={
        "query": "https://www.realtor.com/realestateandhomes-detail/1492-E-57th-St_Brooklyn_NY_11234_M46117-61190",
    },
    timeout=60,
)
response.raise_for_status()
data = response.json()

print(json.dumps(data, indent=2, ensure_ascii=False)[:2000])
```

### TypeScript example

```typescript
type RealtorProperty = {
  id?: string;
  url?: string;
  slug?: string;
  tags?: {
    id?: string;
    label?: string;
  }[];
  agent?: {
    id?: string;
    type?: string;
    agent_id?: string;
    office_id?: string;
    agent_name?: unknown;
    agent_email?: string;
    agent_phone?: unknown;
    office_name?: string;
    office_phone?: unknown;
  }[];
  flags?: {
    is_auction?: unknown;
    is_pending?: boolean;
    is_contingent?: unknown;
    is_non_deeded?: unknown;
    is_short_sale?: unknown;
    is_coming_soon?: unknown;
    is_foreclosure?: unknown;
    is_new_listing?: boolean;
    is_subdivision?: unknown;
    is_price_reduced?: unknown;
    is_usda_eligible?: boolean;
    is_new_construction?: unknown;
    is_fractionally_owned?: unknown;
    is_price_excludes_land?: unknown;
  };
  local?: unknown;
  phones?: unknown[];
  photos?: {
    url?: string;
    tags?: string[];
  }[];
  status?: string;
  details?: {
    beds?: number;
    logo?: unknown;
    name?: unknown;
    pool?: unknown;
    sqft?: unknown;
    text?: string;
    type?: string;
    rooms?: unknown;
    units?: unknown;
    garage?: unknown;
    styles?: unknown;
    zoning?: unknown;
    cooling?: unknown;
    heating?: unknown;
    roofing?: unknown;
    stories?: unknown;
    beds_max?: unknown;
    beds_min?: unknown;
    exterior?: unknown;
    lot_sqft?: number;
    sqft_max?: unknown;
    sqft_min?: unknown;
    sub_type?: unknown;
    baths_max?: unknown;
    baths_min?: unknown;
    [key: string]: unknown;
  };
  history?: unknown;
  features?: {
    bedrooms?: string[];
    bathrooms?: string[];
    "land _info"?: string[];
    "other _rooms"?: string[];
    "interior _features"?: string[];
    "garage and _parking"?: string[];
    "heating and _cooling"?: string[];
    "other _property _info"?: string[];
    "building and _construction"?: string[];
    "exterior and _lot _features"?: string[];
  };
  location?: {
    city?: {
      slug_id?: string;
      county_needed_for_uniq?: boolean;
    };
    county?: {
      name?: string;
      fips_code?: string;
      state_code?: string;
    };
    address?: {
      city?: string;
      line?: string;
      unit?: unknown;
      state?: string;
      country?: string;
      coordinate?: Record<string, unknown>;
      state_code?: string;
      postal_code?: string;
      street_name?: string;
      street_number?: string;
      street_suffix?: string;
      validation_code?: string;
      street_direction?: string;
      street_post_direction?: unknown;
    };
    postal_code?: {
      geo_statistics?: Record<string, unknown>;
    };
    search_areas?: {
      city?: string;
      state_code?: string;
    }[];
    neighborhoods?: {
      name?: string;
    }[];
    street_view_url?: string;
    street_view_metadata_url?: string;
  };
  list_date?: string;
  sold_date?: string;
  list_price?: number;
  sold_price?: number;
  advertisers?: {
    href?: unknown;
    name?: string;
    team?: unknown;
    type?: string;
    email?: string;
    photo?: unknown;
    broker?: {
      logo?: unknown;
      name?: unknown;
      accent_color?: unknown;
      designations?: unknown[];
      fulfillment_id?: string;
    };
    office?: {
      href?: unknown;
      name?: string;
      email?: string;
      hours?: unknown;
      photo?: unknown;
      phones?: unknown;
      slogan?: unknown;
      address?: Record<string, unknown>;
      mls_set?: string;
      lead_email?: unknown;
      fulfillment_id?: string;
      application_url?: unknown;
      out_of_community?: unknown;
    };
    phones?: {
      ext?: unknown;
      type?: string;
      number?: string;
      primary?: boolean;
      trackable?: unknown;
    }[];
    slogan?: unknown;
    address?: {
      city?: unknown;
      line?: unknown;
      state?: unknown;
      country?: unknown;
      state_code?: unknown;
      postal_code?: unknown;
    };
    builder?: unknown;
    mls_set?: string;
    nrds_id?: unknown;
    state_license?: unknown;
    fulfillment_id?: string;
  }[];
  tax_history?: unknown;
  list_price_last_change?: unknown;
};

const params = new URLSearchParams({
  "query": "https://www.realtor.com/realestateandhomes-detail/1492-E-57th-St_Brooklyn_NY_11234_M46117-61190",
});

const response = await fetch(`https://api.piloterr.com/v2/realtor/property?${params}`, {
  headers: { "x-api-key": process.env.PILOTERR_API_KEY! },
});
if (!response.ok) throw new Error(`Piloterr error ${response.status}: ${await response.text()}`);

const data = (await response.json()) as RealtorProperty;

console.log(JSON.stringify(data, null, 2).slice(0, 2000));
```

<details>
<summary><b>POST variant</b></summary>

```http
POST https://api.piloterr.com/v2/realtor/property
x-api-key: YOUR_API_KEY
Content-Type: application/json

{"query": "https://www.realtor.com/realestateandhomes-detail/1492-E-57th-St_Brooklyn_NY_11234_M46117-61190"}
```
</details>

### Output example

Example response from the API reference, abridged — real values depend on the page you scrape.

```json
{
  "id": "2994403623",
  "url": "https://www.realtor.com/realestateandhomes-detail/1492-E-57th-St_Brooklyn_NY_11234_M46117-61190",
  "slug": "1492-E-57th-St_Brooklyn_NY_11234_M46117-61190",
  "tags": [
    {
      "id": "hardwood_floors",
      "label": "Hardwood floors"
    },
    {
      "id": "central_air",
      "label": "Central air"
    }
  ],
  "agent": [
    {
      "id": "BONY",
      "type": "seller",
      "agent_id": "YB6416",
      "office_id": "117980",
      "agent_name": null,
      "agent_email": "yan@topnestinc.com",
      "agent_phone": null,
      "office_name": "Remax Top Nest Real Estate",
      "office_phone": null
    }
  ],
  "flags": {
    "is_auction": null,
    "is_pending": true,
    "is_contingent": null,
    "is_non_deeded": null,
    "is_short_sale": null,
    "is_coming_soon": null,
    "is_foreclosure": null,
    "is_new_listing": false,
    "is_subdivision": null,
    "is_price_reduced": null,
    "is_usda_eligible": false,
    "is_new_construction": null,
    "is_fractionally_owned": null,
    "is_price_excludes_land": null
  },
  "local": null,
  "phones": [],
  "photos": [
    {
      "url": "https://ap.rdcpix.com/3ad76fc1d8db6123926f6cce8a7b838bl-m2523758046s.jpg",
      "tags": [
        "road",
        "porch"
      ]
    }
  ],
  "status": "for_sale",
  "details": {
    "beds": 3,
    "logo": null,
    "name": null,
    "pool": null,
    "sqft": null,
    "text": "2 Family, semi-attached home being delivered vacant. Act now.",
    "type": "multi_family",
    "rooms": null,
    "units": null,
    "garage": null,
    "styles": null,
    "zoning": null,
    "cooling": null,
    "heating": null,
    "roofing": null,
    "stories": null,
    "beds_max": null,
    "beds_min": null,
    "exterior": null,
    "lot_sqft": 1800,
    "sqft_max": null,
    "sqft_min": null,
    "sub_type": null,
    "baths_max": null,
    "baths_min": null
  },
  "history": null,
  "features": {
    "bedrooms": [
      "Bedrooms: 3"
    ],
    "bathrooms": [
      "Full Bathrooms: 1",
      "3/4 Bathrooms: 1"
    ],
    "land _info": [
      "Lot Size Acres: 0.0413223",
      "Lot Size Square Feet: 1800"
    ],
    "other _rooms": [
      "Basement Features: Finished, Full"
    ],
    "interior _features": [
      "A/C Unit",
      "Flooring: Hardwood"
    ],
    "garage and _parking": [
      "Parking Features: 1 Space, Shared Drive"
    ],
    "heating and _cooling": [
      "Cooling Features: 4, AC Units: 4",
      "Heating Fuel: Gas"
    ],
    "other _property _info": [
      "Source Listing Status: Pending",
      "County: Kings (Brooklyn)"
    ],
    "building and _construction": [
      "Building Exterior Type: Brick",
      "Construction Materials: Brick"
    ],
    "exterior and _lot _features": [
      "Yard: Back"
    ]
  },
  "location": {
    "city": {
      "slug_id": "Brooklyn_NY",
      "county_needed_for_uniq": false
    },
    "county": {
      "name": "Kings",
      "fips_code": "36047",
      "state_code": "NY"
    },
    "address": {
      "city": "Brooklyn",
      "line": "1492 E 57th St",
      "unit": null,
      "state": "New York",
      "country": "USA",
      "coordinate": {
        "lat": 40.617188,
        "lon": -73.920186
      },
      "state_code": "NY",
      "postal_code": "11234",
      "street_name": "57th",
      "street_number": "1492",
      "street_suffix": "St",
      "validation_code": "121",
      "street_direction": "E",
      "street_post_direction": null
    },
    "postal_code": {
      "geo_statistics": {
        "housing_market": {}
      }
    },
    "search_areas": [
      {
        "city": "brooklyn",
        "state_code": "ny"
      },
      {
        "city": "new york",
        "state_code": "ny"
      }
    ],
    "neighborhoods": [
      {
        "name": "Flatlands"
      },
      {
        "name": "Southeastern Brooklyn"
      }
    ],
    "street_view_url": "https://maps.googleapis.com/maps/api/streetview?channel=rdc-streetview&key=AIzaSyAP_xs30yS0J4xp8O1ZKUrUttIXKklrwaM&location=1492%20E%2057…",
    "street_view_metadata_url": "https://maps.googleapis.com/maps/api/streetview/metadata?channel=rdc-streetview&key=AIzaSyAP_xs30yS0J4xp8O1ZKUrUttIXKklrwaM&location=1492…"
  },
  "list_date": "2026-04-22T21:24:51Z",
  "sold_date": "1998-03-11",
  "list_price": 500000,
  "sold_price": 175000,
  "advertisers": [
    {
      "href": null,
      "name": "Yan Byshevsky",
      "team": null,
      "type": "seller",
      "email": "example",
      "photo": null,
      "broker": {
        "logo": null,
        "name": null,
        "accent_color": null,
        "designations": [],
        "fulfillment_id": "0"
      },
      "office": {
        "href": null,
        "name": "Top Nest Inc",
        "email": "example",
        "hours": null,
        "photo": null,
        "phones": null,
        "slogan": null,
        "address": {},
        "mls_set": "O-BONY-117980",
        "lead_email": null,
        "fulfillment_id": "0",
        "application_url": null,
        "out_of_community": null
      },
      "phones": [
        {}
      ],
      "slogan": null,
      "address": {
        "city": null,
        "line": null,
        "state": null,
        "country": null,
        "state_code": null,
        "postal_code": null
      },
      "builder": null,
      "mls_set": "A-BONY-YB6416",
      "nrds_id": null,
      "state_license": null,
      "fulfillment_id": "100086239"
    }
  ],
  "tax_history": null,
  "list_price_last_change": null
}
```

### Response fields

| Field | Type | Description |
|---|---|---|
| `id` | string |  |
| `url` | string |  |
| `slug` | string |  |
| `tags[]` | object[] |  |
| `tags[].id` | string |  |
| `tags[].label` | string |  |
| `agent[]` | object[] |  |
| `agent[].id` | string |  |
| `agent[].type` | string |  |
| `agent[].agent_id` | string |  |
| `agent[].office_id` | string |  |
| `agent[].agent_name` | object |  |
| `agent[].agent_email` | string |  |
| `agent[].agent_phone` | object |  |
| `agent[].office_name` | string |  |
| `agent[].office_phone` | object |  |
| `flags` | object |  |
| `flags.is_auction` | object |  |
| `flags.is_pending` | boolean |  |
| `flags.is_contingent` | object |  |
| `flags.is_non_deeded` | object |  |
| `flags.is_short_sale` | object |  |
| `flags.is_coming_soon` | object |  |
| `flags.is_foreclosure` | object |  |
| `flags.is_new_listing` | boolean |  |

## Realtor Search API

Search Realtor.com listings from a search URL and retrieve prices, beds, baths, sqft, photos, and property metadata.

`GET | POST https://api.piloterr.com/v2/realtor/search` · **2 credits per request** · [Full reference](https://app.piloterr.com/openapi)

### Request parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `query` | string | ✅ | Full Realtor.com search results URL. |

### Python example

```python
import json
import os
import requests

response = requests.get(
    "https://api.piloterr.com/v2/realtor/search",
    headers={"x-api-key": os.environ["PILOTERR_API_KEY"]},
    params={
        "query": "https://www.realtor.com/realestateandhomes-search/New-York_NY",
    },
    timeout=60,
)
response.raise_for_status()
data = response.json()

print(json.dumps(data, indent=2, ensure_ascii=False)[:2000])
```

### TypeScript example

```typescript
type RealtorSearch = {
  results?: {
    photos?: {
      href?: string;
    }[];
    location?: {
      address?: Record<string, unknown>;
    };
    permalink?: string;
    list_price?: number;
    description?: {
      beds?: number;
      sqft?: number;
      type?: string;
      baths?: number;
      lot_size?: number;
    };
    property_id?: string;
  }[];
};

const params = new URLSearchParams({
  "query": "https://www.realtor.com/realestateandhomes-search/New-York_NY",
});

const response = await fetch(`https://api.piloterr.com/v2/realtor/search?${params}`, {
  headers: { "x-api-key": process.env.PILOTERR_API_KEY! },
});
if (!response.ok) throw new Error(`Piloterr error ${response.status}: ${await response.text()}`);

const data = (await response.json()) as RealtorSearch;

console.log(JSON.stringify(data, null, 2).slice(0, 2000));
```

<details>
<summary><b>POST variant</b></summary>

```http
POST https://api.piloterr.com/v2/realtor/search
x-api-key: YOUR_API_KEY
Content-Type: application/json

{"query": "https://www.realtor.com/realestateandhomes-search/New-York_NY"}
```
</details>

### Output example

Example response from the API reference, abridged — real values depend on the page you scrape.

```json
{
  "results": [
    {
      "photos": [
        {}
      ],
      "location": {
        "address": {}
      },
      "permalink": "299-Troutman-St_Brooklyn_NY_11237_M99576-61733",
      "list_price": 500000,
      "description": {
        "beds": 16,
        "sqft": 6500,
        "type": "SingleFamilyResidence",
        "baths": 8,
        "lot_size": 2500
      },
      "property_id": "9957661733"
    },
    {
      "photos": [
        {}
      ],
      "location": {
        "address": {}
      },
      "permalink": "D132-Edgewater-Unit-D_Bronx_NY_10465_M94332-74355",
      "list_price": 255000,
      "description": {
        "beds": 4,
        "sqft": 1200,
        "type": "SingleFamilyResidence",
        "baths": 1,
        "lot_size": null
      },
      "property_id": "9433274355"
    }
  ]
}
```

### Response fields

| Field | Type | Description |
|---|---|---|
| `results[]` | object[] |  |
| `results[].photos[]` | object[] |  |
| `results[].location` | object |  |
| `results[].permalink` | string |  |
| `results[].list_price` | integer |  |
| `results[].description` | object |  |
| `results[].property_id` | string |  |

## Code examples in other languages

Ready-to-run examples live in the [`examples/`](examples) folder. Each one reads your key from the `PILOTERR_API_KEY` environment variable.

| Language | Realtor Property | Realtor Search |
|---|---|---|
| cURL (Bash) | [`property`](examples/curl/property.sh) | [`search`](examples/curl/search.sh) |
| PHP | [`property`](examples/php/property.php) | [`search`](examples/php/search.php) |
| C# | [`property`](examples/csharp/Property.cs) | [`search`](examples/csharp/Search.cs) |
| Go | [`property`](examples/go/property.go) | [`search`](examples/go/search.go) |
| Java | [`property`](examples/java/PropertyExample.java) | [`search`](examples/java/SearchExample.java) |
| Ruby | [`property`](examples/ruby/property.rb) | [`search`](examples/ruby/search.rb) |
| Node.js | [`property`](examples/nodejs/property.mjs) | [`search`](examples/nodejs/search.mjs) |

## Practical use cases

- **Price monitoring** — Track asking prices and price drops per area.
- **Market analytics** — Measure inventory, days on market and price per m² / sqft.
- **Investment sourcing** — Detect undervalued properties as soon as they are listed.
- **Rental yield models** — Combine sale and rent listings to estimate yields.
- **Proptech products** — Power portals, valuation tools and alerts with structured listings.

## Why Piloterr?

- **No infrastructure** — no proxies, headless browsers or CAPTCHA solving to run yourself.
- **Structured JSON** — stable, documented fields instead of brittle HTML selectors.
- **Pay per request** — transparent credit cost per endpoint, failed requests are retried for you.
- **One API key, hundreds of sources** — Realtor.com plus many other e-commerce, search and company data endpoints in the [Piloterr library](https://www.piloterr.com/library).
- **Any language** — plain HTTPS + JSON, with examples for Python, TypeScript, cURL, PHP, C#, Go, Java, Ruby and Node.js.

## FAQ

### Is it legal to scrape Realtor.com?

Collecting publicly available data is generally allowed in many jurisdictions, but rules depend on your country, the data you collect and how you use it. Avoid personal data unless you have a lawful basis, respect the website's terms where they apply, and get legal advice for your specific use case. This is not legal advice.

### Do I need proxies or a headless browser?

No. Piloterr handles rendering, proxy rotation and retries on its side. You only send an HTTPS request with your `x-api-key` header and receive JSON.

### How much does a request cost?

Credits per call: `/v2/realtor/property` **2**, `/v2/realtor/search` **2**. See the [Piloterr website](https://www.piloterr.com) for plans.

### What data does the Realtor.com API return?

Each endpoint returns structured JSON: **Realtor Property** — `id`, `url`, `slug`, `tags[]`, `tags[].id`, `tags[].label`; **Realtor Search** — `results[]`, `results[].photos[]`, `results[].location`, `results[].permalink`, `results[].list_price`, `results[].description`.

### Which languages are supported?

Any language that can make an HTTP request. This README shows Python and TypeScript; the [`examples/`](examples) folder contains cURL, PHP, C#, Go, Java, Ruby and Node.js.

## Related scrapers

- [Apartments Scraper API](https://github.com/piloterr/apartments-scraper)
- [Argenprop Scraper API](https://github.com/piloterr/argenprop-scraper)
- [Centris Scraper API](https://github.com/piloterr/centris-scraper)
- [Fotocasa Scraper API](https://github.com/piloterr/fotocasa-scraper)
- [Funda Scraper API](https://github.com/piloterr/funda-scraper)
- [Homestra Scraper API](https://github.com/piloterr/homestra-scraper)
- [All Piloterr scrapers on GitHub](https://github.com/piloterr)

## Support

- 💬 Join the [Piloterr Discord](https://discord.gg/CFj3ph8aHU) to ask questions and share what you build.
- 📚 Browse the [API reference (OpenAPI)](https://app.piloterr.com/openapi) and the [Piloterr library](https://www.piloterr.com/library).
- 🔑 [Get your API key](https://app.piloterr.com).

---

<p align="center">
  <a href="https://www.piloterr.com">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="images/logo-dark.svg">
      <img src="images/logo.svg" alt="Piloterr" height="32">
    </picture>
  </a>
  <br>
  <sub>Built by <a href="https://www.piloterr.com">Piloterr</a> — web scraping APIs for e-commerce, search, real estate and more, one API key.</sub>
</p>

<sub>Realtor.com is a trademark of its respective owner. This repository is not affiliated with or endorsed by Realtor.com. Examples are released under the MIT license.</sub>
