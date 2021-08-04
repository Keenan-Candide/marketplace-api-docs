# Orders

## Get Orders

> Example Request

```shell
curl "https://marketplace-api.candideapp.com/v1/orders" \
  -X GET \
  -H 'Content-Type: application/json' \
  -H "Authorization: plants-plants-plants"
```

> Response

```json
{
  "items": [
    {
      "id": "e6620e75-ee7d-41c9-95c8-646172ffc9be",
      "status": "OPEN",
      "paymentStatus": "PAID",
      "subtotal": 12500,
      "postage": 500,
      "total": 13000,
      "currencyCode": "GBP",
      "totalItems": 1,
      "buyerName": "Test Buyer",
      "buyerEmail": "test.buyer@candide.eu",
      "shippingAddress": {
        "line1": "123 Buyer Street",
        "line2": null,
        "city": "Bristol",
        "postcode": "BS3 123",
        "country": "GB"
      },
      "lineItems": [
        {
          "listingId": "e98203c7-2170-4d3b-a080-8429dccf62e5",
          "sku": "SKU-00001",
          "quantity": 1,
          "unitPrice": 12500,
          "refunded": 0,
          "title": "Test Listing"
        }
      ],
      "createdAt": "2021-07-19T11:50:17.713Z",
      "updatedAt": "2021-07-19T11:50:17.713Z"
    }
  ],
  "nextCursor": "eyJpZCI6ImUzZjFlYTg5LWM0ZDMtNGQ5Ni1iNGQ3LTg1ZWNlNTJjY2YxYyIsImNyZWF0ZWRBdCI6IjIwMjAtMTEtMDRUMTM6NTk6MzYuNzM1WiJ9"
}
```

You can retrieve open orders in batches of 50 at a time.

### HTTP Request

`GET https://marketplace-api.candideapp.com/v1/orders`

### Arguments

| Parameter                | Type   | Description                                                                           |
| ------------------------ | ------ | ------------------------------------------------------------------------------------- |
| after                    | string | An optional cursor provided to fetch the next page                                    |

<aside class="notice">
Currently only retrieving open orders is supported.
</aside>

## Mark Order as Dispatched

> Example Request

```shell
curl "https://marketplace-api.candideapp.com/v1/orders/352de449-a943-4651-937b-52b7ad3246e6/dispatch" \
  -X POST \
  -H 'Content-Type: application/json' \
  -H "Authorization: plants-plants-plants" \
  -d '{"note": "Your package will arrive in 2-3 days."}'
```

> Response

```json
{
  "id": "352de449-a943-4651-937b-52b7ad3246e6",
  "status": "DISPATCHED",
  "updatedAt": "2021-06-17T15:53:14.735Z"
}
```

Marks an order as dispatched and sends an email to the buyer with the provided note (if supplied).

### HTTP Request

`POST https://marketplace-api.candideapp.com/v1/orders/<ID>/dispatch`

### URL Parameters

| Parameter        | Description                                 |
| ---------------- | ------------------------------------------- |
| id _(required)_  | The ID of the order |

### Arguments

| Parameter | Type   | Description                                                                           |
| --------- | ------ | ------------------------------------------------------------------------------------- |
| note      | string | An optional note to be included in the email to the buyer                             |
