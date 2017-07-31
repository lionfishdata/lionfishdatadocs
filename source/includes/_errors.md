# Errors

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

