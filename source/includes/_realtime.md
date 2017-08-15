# Get realtime product info

Get critical product data delivered realtime including title, description, price, and more for any product on **Amazon** (more retailers coming soon).

> Example realtime product info request

```shell
curl https://api.lionfishdata.com/v1/products/B00W9FLKTY/fast?retailer=amazon \
  -u <client_token>:
```

To retrieve product info, make a GET request to the following URL, replacing `:product_id` with the retailer's unique identifier for a particular product and specifying the request attributes as query parameters in the URL

`https://api.lionfishdata.com/v1/products/:product_id/fast?retailer=amazon`

### Authentication

You authenticate your account by including your [client token](https://www.lionfishdata.com/user/-/realtime/try) in your request. Authentication is performed through HTTP Basic Auth, where the client token is the basic auth username value. You do not need to provide a password.

### Required request attributes

Attribute | Type | Description
--------- | ---- | -----------
retailer | String | The retailer for the product

### Optional request attributes

Attribute | Type | Description
--------- | ---- | -----------
timeout | Number | Number of seconds to process the request before aborting (default 60 seconds).
max_age | Number | The data returned in the response will be at most this many seconds old. The minimum is 30 seconds. **To take full advantage of caching set this value based on your application's requirements.**

> Example product info response

```shell
{
  "status": "completed",
  "original_retail_price": 3797,
  "timestamp": 1501535860,
  "retailer": "amazon",
  "feature_bullets": [
    "USB 3.0 4 ports super speed hub for computer/notebook. Drive free, supports: Windows (XP/Vista/7/8/8.1/10), Mac OSx(10.x and above), and Linux.",
    "The built-in intelligent USB charging port (2A/1A), has an intelligent auto switching chip."
  ],
  "images": [
    "https://images-na.ssl-images-amazon.com/images/I/71CpWUVHpyL.jpg",
    "https://images-na.ssl-images-amazon.com/images/I/711M8uk%2BYVL.jpg"
  ],
  "package_dimensions": {
    "weight": {
      "amount": 3.2,
      "unit": "ounces"
    },
    "size": {
      "width": {
        "amount": 8.7,
        "unit": "inches"
      },
      "depth": {
        "amount": 41.3,
        "unit": "inches"
      },
      "length": {
        "amount": 16.5,
        "unit": "inches"
      }
    }
  },
  "price": 1399,
  "question_count": 115,
  "asin": "B00W9FLKTY",
  "ship_price": 0,
  "main_image": "https://images-na.ssl-images-amazon.com/images/I/71CpWUVHpyL.jpg",
  "review_count": 582,
  "product_id": "B00W9FLKTY",
  "title": "USB 3.0 Hub, atolla 4 Ports Super Speed USB 3 Hub Splitter With On Off Switch With 1 USB Charging Port (Cable Length 2 Feet, No AC adapter)",
  "MPN": "CH-204U3",
  "product_description": "Color:4-Port Hub without AC adapter           The Perfect USB 3.0 HUB you ever\nneed   SuperSpeed Sync and Dynamic FastCharging: Extend 4 more USB 3.0 Ports +\n1 Fast Charger Port (up to 2.1 Amps) Unplugging-Free: Individual on/off switch\nturns off port whenever you don't need it.  Vertical USB Port provides\nadditional space for \"fat\" USB devices and plugs Nice Design, Solid Built with\na strong cable of 26\" length.  Provide one 5V DC port for an additional power\nadapter.",
  "product_details": [
    "Product Dimensions: 41.3 x 16.5 x 8.7 inches",
    "Item Weight: 3.2 ounces"
  ],
  "categories": [
    "Electronics",
    "Computers & Accessories"
  ],
  "stars": null,
  "brand": "Atolla",
  "variant_specifics": [
    {
      "dimension": "Color",
      "value": "4-Port Hub without AC adapter"
    }
  ],
  "all_variants": [
    {
      "variant_specifics": [
        {
          "dimension": "Color",
          "value": "4-Port Hub without AC adapter"
        }
      ],
      "product_id": "B00W9FLKTY"
    }
  ]
}
```

### Response attributes

Attribute | Type | Description
--------- | ---- | -----------
status | String | Possible values are `processing`, `failed`, or `completed`
retailer | String | The retailer for the product
product_id | String | The retailer's unique identifier for the product
price | Number | The price of the product (buy box)
ship_price | Number | The price to ship the product (buy box)
title | String | Title of the product
main_image | String | The URL of the primary image associated with the product
images | Array | An array of image URLs associated with the product
variant_specifics | Array | Array of objects containing information about the types and values of product variants available. A variant specifics object contains a `dimension` field describing the type of the variant (e.g. "Color") and a `value` field describing the specific value available
product_description | String | The description of the product
timestamp | String | The timestamp that the resource was accessed

### Errors

> Example error response

```shell
{
  "_type": "error",
  "code": "product_unavailable",
  "message": "One of the products you selected is unavailable.",
  "data": {'product_id': '018293801'}
}
```

If there is an error processing a request, the result endpoint will return an error object containing three fields: `code`, `message`, and `data`.

The `code` field provides a short, unique error code describing the error situation. The `message` field provides a human readable message describing the error and is intended for the developer and not the end user. The `data` field contains specific information related to the error (for example, the maximum quantity allowed and the desired quantity would be shown for a `max_quantity_exceeded` error).

The LionFish API uses the following errors:

Error Code | Meaning
---------- | -------
expired_product_id | The product_id you used is no longer supported by the retailer.
insufficient_variants | You did not select all required variants for a product.
internal_error | LionFish or the retailer you requested is experiencing outages. Please try again or contact support@lionfishdata.com if this error persists.
invalid_client_token |  Your client token is invalid.
invalid_json | The JSON in your request could not be parsed.
invalid_request | Validation failed on the request.
invalid_variant | One of the product variants you provided was not valid.
unauthorized_access | You are not authorized to make this API call. Please contact support@lionfishdata.io.

