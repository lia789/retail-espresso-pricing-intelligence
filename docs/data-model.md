##  **Product Data Model**

```
Each collected product will contain:

| Field | Type | Required |
|---|---|---|
| source | string | Yes |
| product_id | string | Yes |
| brand | string | No |
| product_name | string | Yes |
| price | decimal | Yes |
| original_price | decimal | No |
| currency | string | Yes |
| availability | string | Yes |
| product_url | string | Yes |
| observed_at | datetime | Yes |
```

## Availability Values
```
Initially:
- IN_STOCK
- OUT_OF_STOCK
```


## Product Identity
```
A product should be uniquely identified within a retailer using:

source + product_id

If a retailer does not provide a reliable product ID, we will later define a stable generated identifier.
```