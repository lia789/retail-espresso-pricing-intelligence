# **Whole Latte Love Source Investigation**

## **URL Structure**

```text
# Base URL
https://www.wholelattelove.com/collections/espresso-machines

# Pagination
https://www.wholelattelove.com/collections/espresso-machines?page=0
https://www.wholelattelove.com/collections/espresso-machines?page=1
```

## **Data Source**

Uses Algolia JSON API.

```text
POST
https://qb0bcna4eq-dsn.algolia.net/1/indexes/*/queries
```

Pagination starts from `page=0`.

```text
hitsPerPage=40
```

## **Data Fields**

```text
product_id      -> id
product_name    -> title
brand           -> vendor
price           -> price
original_price  -> compare_at_price
availability    -> inventory_available
product_url     -> built from handle
currency        -> USD
```

## **Scraping Investigation**

```text
Algolia JSON API
No individual product-page request required.
All required product data is available from the API.
```

## **Python Test Code**

```python
import requests
from datetime import datetime, timezone
from urllib.parse import urlencode
import json


API_URL = "https://qb0bcna4eq-dsn.algolia.net/1/indexes/*/queries"

API_PARAMS = {
    "x-algolia-api-key": "d00e8a983bebaef76b2c540c5382a175",
    "x-algolia-application-id": "QB0BCNA4EQ",
}

HITS_PER_PAGE = 40


def fetch_page(page):
    query_params = {
        "page": page,
        "hitsPerPage": HITS_PER_PAGE,
        "filters": "meta.algolia.ignore:public AND collections:espresso-machines",
        "distinct": "true",
        "attributesToRetrieve": json.dumps([
            "id",
            "handle",
            "title",
            "price",
            "compare_at_price",
            "inventory_available",
            "vendor",
        ]),
    }

    payload = {
        "requests": [
            {
                "indexName": "shopify_wllusproducts",
                "query": "",
                "params": urlencode(query_params),
            }
        ]
    }

    response = requests.post(
        API_URL,
        params=API_PARAMS,
        json=payload,
        timeout=30,
    )

    response.raise_for_status()

    return response.json()["results"][0]


def parse_product(item):
    handle = item.get("handle")

    return {
        "source": "whole_latte_love",
        "product_id": str(item.get("id")),
        "brand": item.get("vendor"),
        "product_name": item.get("title"),
        "price": item.get("price"),
        "original_price": item.get("compare_at_price"),
        "currency": "USD",
        "availability": item.get("inventory_available"),
        "product_url": (
            f"https://www.wholelattelove.com/products/{handle}"
            if handle else None
        ),
        "observed_at": datetime.now(timezone.utc).isoformat(),
    }


page = 0
products = []

while True:
    result = fetch_page(page)

    for item in result["hits"]:
        products.append(parse_product(item))

    page += 1

    if page >= result["nbPages"]:
        break


for product in products:
    print(product)
```