# **Retail Espresso Pricing Intelligence Business Requirements**


## Business Problem
```
The pricing team needs a reliable daily view of espresso machine prices and availability across selected online retailers.

The system should reduce the need for manually checking competitor websites and make it possible to understand how prices, availability, and product catalogs change over time.
```

## Target Retailers
```
The initial retailers are:
- Clive Coffee
- Whole Latte Love
- Seattle Coffee Gear
- Espresso Coffee Shop
- 1st-line Equipment

Only espresso machines are in scope. Other product categories not be included.
```


## Collection Requirements
```
The system must:

1. collect the current espresso machine catalog from each retailer once per day
2. record when each product was observed
3. collect approximately 500 fresh product observations per day across all sources
```


## Product Data Requirements
```
Each product observation should contain:

- retailer/source
- product ID or SKU when available
- brand
- product/model name
- current selling price
- original/list price when available
- currency
- availability
- product page URL
- observation date and time

If a retailer does not provide a reliable product ID, the system must still be able to identify the product consistently for that retailer.
```


## Change Detection Requirements
```
The system must identify important product changes. Example:
- NEW_PRODUCT
- PRICE_DROP
- PRICE_INCREASE
- OUT_OF_STOCK
- BACK_IN_STOCK
- PRODUCT_MISSING

Price-change records should include:
- previous price
- current price
- price difference
- percentage change
```

## Crawl Health Requirements
```
Each source crawl must record:
- source
- crawl date
- number of products found
- number of valid products
- number of failed products
- crawl status

A large unexpected drop in discovered products should be treated as a possible crawler or source problem before products are classified as missing.
```


## Data Access Requirements
```
The collected data and detected changes must be stored in a form that can be queried by analysts and other internal systems.

The system should support access to:
- today's products
- current competitor prices
- historical prices
- current availability
- price drops
- price increases
- new products
- stock changes
- missing products
- crawl health
```


## Expected Output
```
The final system should provide the pricing team with a reliable and queryable view of competitor espresso machine pricing, availability, historical changes, and crawl health.
```
