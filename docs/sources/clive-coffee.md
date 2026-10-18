# **Clive Coffee Source Investigation**


## **Url Structure**

```
# Base URL
https://clivecoffee.com/collections/espresso-machines

# Pagination
https://clivecoffee.com/collections/espresso-machines?page=1
https://clivecoffee.com/collections/espresso-machines?page=2

# Product Page
https://clivecoffee.com/collections/espresso-machines/products/rocket-espresso-boxer-timer-commercial-espresso-machine-2-group
Note: It have availability
In stock, and ready to ship
Only 2 left. Order soon!
Lead Time: Up to Three Weeks
```


## **Data Field**

```
product_id     -> generated from product URL handle
product_name
brand
price
product_url
```

## **Scraping Investigations**
```
Static website with paginations!
```


## **XPATH Code**
```
product = selector.xpath(
    "(//div[contains(concat(' ', normalize-space(@class), ' '), ' product-item ')])[1]"
)

product_name = product.xpath(
    "normalize-space(.//h4[contains(@class, 'product-item__product-title')]/a)"
).get()
print(product_name)

brand = product.xpath(
    "normalize-space(.//h5[contains(@class, 'product-item__product-vendor')])"
).get()
print(brand)

price = product.xpath(
    "normalize-space(.//p[contains(@class, 'product-item__price')]/span[contains(@class, 'product-item__price')])"
).get()
print(price)

product_url = product.xpath(
    "normalize-space(.//button[@data-quick-shop-trigger='quick-view'][1]/@data-product-url)"
).get()
print(product_url)
```


