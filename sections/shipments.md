Shipments
=========

Endpoints:

- [Get all shipments](#get-all-shipments)
- [Count shipments](#count-shipments)
- [Get a shipment](#get-a-shipment)
- [Create a shipment](#create-a-shipment)
- [Delete a shipment](#delete-a-shipment)
- [Buy postage](#buy-postage)
- [Refund postage](#refund-postage)
- [Add shipments to a batch](#add-shipments-to-a-batch)
- [Remove shipments from a batch](#remove-shipments-from-a-batch)


Get all shipments
-----------------

* `GET /shipments` will return a [paginated list][pagination] of shipments belonging to the client sorted by most recently created shipment first.

_Optional parameters_:

* `batch` (integer) - when set return shipments that belong to the given batch.

* `from_date` (date) - when set return shipments with a `created_at` on or after the given date.

* `limit` (integer) - number of records to return per page (default is 100).

* `page` (integer) - pagination page number (default is 1).

* `q` (string) - allows for full text searching of shipments by `shipment_id`, `to_address_name`, or `order_id`.

* `state` (enum) - allows for searching shipments based on the following states:
  * `canceled` - the shipment has been canceled to prevent delivery and will either be held at a branch or returned to the client.
  * `pending` - the shipment is in the process of being created by the client. Shipments in this state cannot be received by Chat Chats.
  * `ready` - the shipment is ready to be received by Chit Chats. This means the postage has been purchased or provided.
  * `in_transit` - the shipment is in the process of being delivered. The following three statuses can be used to filter with greater detail:
    * `received` - the shipment has been received by Chit Chats.
    * `released` - Chit Chats has released the shipment to the carrier.
    * `inducted` - shipment is confirmed by tracking event to be in possesion by the shipping carrier.
  * `resolved` - the shipment has been resolved. The following three statuses can be used to filter with greater detail:
    * `delivered` - resolved as delivered.
    * `exception` - resolved as exception meaning that there may have been a problem deliverying the shipment. It doesn't always mean the shipment was not delivered.
    * `voided` - resolved as voided because a postage refund was requested.

* `to_date` (date) - when set only return shipments with a `created_at` greater than or equal to the given date.

###### Example JSON Response
```json
[
  {
    "shipment_id": "ABCDE12345",
    "status": "ready",
    ...
  },
  {
    "shipment_id": "Q5P4R3S2T1",
    "status": "pending",
    ...
  }
]
```

###### Copy as cURL
``` shell
curl -H "Authorization: $ACCESS_TOKEN" \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/shipments"
```


Count shipments
---------------

* `GET /shipments/count` will return number of shipments. You can pass the `state` parameter in [Get all shipments](#get-all-shipments) to count shipments in a specific state.

###### Example JSON Response
```json
{
  "count": 2
}
```


Get a shipment
--------------

* `GET /shipments/1by4s9h87b` will return the shipment with the given ID, granted they have access to it.

The `tracking_details` key contains an array of the tracking evens for the shipment.

###### Example JSON Response
```json
{
  "shipment_id": "1BY4S9H87B",
  "status": "postage_unpaid",
  "to_name": "Jane Doe",
  "to_address_1": "123 ANYWHERE ST.",
  "to_address_2": null,
  "to_city": "VANCOUVER",
  "to_province_code": "BC",
  "to_postal_code": "V6K 1A1",
  "to_country_code": "CA",
  "to_phone": null,
  "return_name": "Shaw Corp",
  "return_address_1": "205-1925 NELSON ST",
  "return_address_2": null,
  "return_city": "VANCOUVER",
  "return_province_code": "BC",
  "return_postal_code": "V6G 1N3",
  "return_country_code": "CA",
  "return_phone": "1-844-842-8777",
  "package_contents": "merchandise",
  "description": "Hand made bracelet",
  "value": "85.0",
  "value_currency": "USD",
  "order_id": null,
  "order_store": null,
  "package_type": "parcel",
  "size_unit": "cm",
  "size_x": "10.0",
  "size_y": "5.0",
  "size_z": "2.0",
  "weight_unit": "g",
  "weight": "250.0",
  "insured": false,
  "signature_requested": false,
  "postage_type": "unknown",
  "carrier": "unknown",
  "carrier_tracking_code": null,
  "tracking_url": "https://chitchats.com/tracking/1by4s9h87b",
  "ship_date": "2018-01-27",
  "purchase_amount": "8.66",
  "provincial_tax": null,
  "provincial_tax_label": null,
  "federal_tax": "0.41",
  "federal_tax_label": "GST (5%)",
  "postage_fee": "8.66",
  "insurance_fee": null,
  "delivery_fee": null,
  "created_at": "2018-01-27T11:26:41.045-08:00",
  "postage_label_png_url": null,
  "postage_label_zpl_url": null,
  "tracking_events": [
    {
      "type": "create_shipment",
      "title": "Shipment created",
      "subtitle": null,
      "location_description": null,
      "created_at": "2018-01-27T11:26:41.056-08:00",
      "status": null
    }
  ]
}
```

###### Copy as cURL
``` shell
curl -H "Authorization: $ACCESS_TOKEN" \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/shipments/1by4s9h87b"
```


Create a shipment
-----------------

* `POST /shipments` with the required parameters (see example) to create a new shipment.

###### Example JSON Request
``` json
{
  "name": "Jane Doe",
  "address_1": "123 ANYWHERE ST.",
  "address_2": "",
  "city": "Vancouver",
  "province_code": "BC",
  "postal_code": "V6K 1A1",
  "country_code": "CA",
  "phone": "800-555-1212",
  "return_us_address": "",
  "package_contents": "merchandise",
  "description": "Hand made bracelet",
  "value": "85",
  "value_currency": "usd",
  "order_id": "",
  "order_store": "",
  "package_type": "parcel",
  "weight_unit": "g",
  "weight": "250",
  "size_unit": "cm",
  "size_x": "10",
  "size_y": "5",
  "size_z": "2",
  "insurance_requested": "yes",
  "signature_requested": "no",
  "postage_type": "chit_chats_canada_tracked",
  "tracking_number": "",
  "ship_date": "today"
}
```

This will return `201 Created` with the URL of the shipment in the `Location` header if the creation was a success. See the [Get a shipment](#get-a-shipment) endpoint for more info.

###### Copy as cURL
``` shell
curl -X POST \
  -H "Authorization: $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Jane Doe",
    "address_1": "123 ANYWHERE ST.",
    "city": "Vancouver",
    "province_code": "BC",
    "postal_code": "V6K 1A1",
    "country_code": "CA",
    "description": "Hand made bracelet",
    "value": "85",
    "value_currency": "usd",
    "package_type": "parcel",
    "size_unit": "cm",
    "size_x": "10",
    "size_y": "5",
    "size_z": "2",
    "weight_unit": "g",
    "weight": "250",
    "postage_type": "chit_chats_canada_tracked",
    "ship_date": "today"
  }' \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/shipments"
```


Delete a shipment
-----------------

* `DELETE /shipments/abcde12345` will delete the pending shipment with the given ID if allowed. If the shipment has purchased postage or has been received by Chit Chats the shipment cannot be deleted but it can be refunded to void the shipment. No parameters required. Returns `204 No Content` if successful.

###### Copy as cURL

``` shell
curl -s -X DELETE \
  -H "Authorization: $ACCESS_TOKEN" \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/shipments/abcde12345"
```


Add shipments to a batch
------------------------

* `PATCH /shipments/add_to_batch` will add the given shipments to the given batch. Returns `200 OK` if successful.

###### Example JSON Request
``` json
{
  "batch": 1,
  "shipment_ids": [
    "ABCDE12345",
    "Q5P4R3S2T1"
  ]
}
```

###### Copy as cURL
``` shell
curl -s -X PATCH \
  -H "Authorization: $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "batch": 1,
    "shipment_ids": [
      "ABCDE12345",
      "Q5P4R3S2T1"
    ]
  }' \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/shipments/add_to_batch"
```


Remove shipments from a batch
-----------------------------

* `PATCH /shipments/remove_from_batch` will remove shipments for the batch they belong to. Returns `200 OK` if successful.

###### Example JSON Request
``` json
{
  "shipment_ids": [
    "ABCDE12345",
    "Q5P4R3S2T1"
  ]
}
```

###### Copy as cURL
``` shell
curl -s -X PATCH \
  -H "Authorization: $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "shipment_ids": [
      "ABCDE12345",
      "Q5P4R3S2T1"
    ]
  }' \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/shipments/remove_from_batch"
```


[pagination]: https://github.com/chitchats/chitchats-api-doc/blob/master/README.md#pagination
