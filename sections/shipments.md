Shipments
=========

Endpoints:

- [Get all shipments](#get-all-shipments)
- [Count shipments](#count-shipments)
- [Get a shipment](#get-a-shipment)
- [Create a shipment](#create-a-shipment)
- [Delete a shipment](#delete-a-shipment)
- [Refresh a shipment](#refresh-a-shipment)
- [Buy shipment](#buy-shipment)
- [Refund shipment](#refund-shipment)
- [Add shipments to a batch](#add-shipments-to-a-batch)
- [Remove shipments from a batch](#remove-shipments-from-a-batch)


Get all shipments
-----------------

* `GET /shipments` will return a [paginated list][pagination] of shipments belonging to the client sorted by most recently created shipment first.

_Optional parameters_:

* `batch_id` (integer) - when set return shipments that belong to the given batch.

* `from_date` (date) - when set return shipments with a `created_at` on or after the given date.

* `limit` (integer) - number of records to return per page (default is 100).

* `page` (integer) - pagination page number (default is 1).

* `q` (string) - allows for full text searching of shipments by `shipment_id`, `to_address_name`, or `order_id`.

* `status` (enum) - allows for searching shipments based on the following states:
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
    "id": "8ERNJ8SCQ9",
    "status": "received",
    "batch_id": 2,
    "to_name": "15Adam Lawrence",
    "to_address_1": "1874 CRITTENDEN RD, APT 7",
    "to_address_2": null,
    "to_city": "ROCHESTER",
    "to_province_code": "WA",
    "to_postal_code": "14623",
    "to_country_code": "US",
    "to_phone": null,
    "return_name": "AMISTAD NATIONAL RECREATION AREA",
    "return_address_1": "4121 VETERANS BLVD",
    "return_address_2": null,
    "return_city": "DEL RIO",
    "return_province_code": "TX",
    "return_postal_code": "78840-3384",
    "return_country_code": "US",
    "return_phone": "1-844-842-8777",
    "package_contents": "merchandise",
    "description": "Statue and documents in crate",
    "value": "20.00",
    "value_currency": "USD",
    "order_id": null,
    "order_store": null,
    "package_type": "parcel",
    "size_unit": "cm",
    "size_x": 28.0,
    "size_y": 21.0,
    "size_z": 21.0,
    "weight_unit": "g",
    "weight": 1850.0,
    "is_insured": false,
    "is_signature_requested": false,
    "postage_type": "usps_priority",
    "carrier": "usps",
    "carrier_tracking_code": "9405536895357112578988",
    "tracking_url": "https://chitchats.com/tracking/8ernj8scq9",
    "ship_date": "2017-11-15",
    "purchase_amount": "22.39",
    "provincial_tax": null,
    "provincial_tax_label": null,
    "federal_tax": null,
    "federal_tax_label": null,
    "postage_fee": "22.39",
    "insurance_fee": null,
    "delivery_fee": "1.00",
    "created_at": "2017-11-14T11:04:32.168-08:00",
    "postage_label_png_url": "https://chitchats.com/labels/shipments/8ernj8scq9.png",
    "postage_label_zpl_url": "https://chitchats.com/labels/shipments/8ernj8scq9.zpl"
  },
  {
    "id": "R94DT3F7DK",
    "status": "received",
    "batch_id": 2,
    "to_name": "14Adam Lawrence",
    "to_address_1": "1874 CRITTENDEN RD, APT 7",
    "to_address_2": null,
    "to_city": "ROCHESTER",
    "to_province_code": "WA",
    "to_postal_code": "14623",
    "to_country_code": "US",
    "to_phone": null,
    "return_name": "APOSTLE ISLANDS NATIONAL LAKESHORE",
    "return_address_1": "415 WASHINGTON AVE",
    "return_address_2": null,
    "return_city": "BAYFIELD",
    "return_province_code": "WI",
    "return_postal_code": "54814-4809",
    "return_country_code": "US",
    "return_phone": "1-844-842-8777",
    "package_contents": "merchandise",
    "description": "Statue and documents in crate",
    "value": "20.00",
    "value_currency": "USD",
    "order_id": null,
    "order_store": null,
    "package_type": "parcel",
    "size_unit": "cm",
    "size_x": 28.0,
    "size_y": 21.0,
    "size_z": 21.0,
    "weight_unit": "g",
    "weight": 1850.0,
    "is_insured": false,
    "is_signature_requested": false,
    "postage_type": "usps_priority",
    "carrier": "usps",
    "carrier_tracking_code": "9405536895357112579015",
    "tracking_url": "https://chitchats.com/tracking/r94dt3f7dk",
    "ship_date": "2017-11-15",
    "purchase_amount": "22.39",
    "provincial_tax": null,
    "provincial_tax_label": null,
    "federal_tax": null,
    "federal_tax_label": null,
    "postage_fee": "22.39",
    "insurance_fee": null,
    "delivery_fee": "1.00",
    "created_at": "2017-11-14T11:03:58.774-08:00",
    "postage_label_png_url": "https://chitchats.com/labels/shipments/r94dt3f7dk.png",
    "postage_label_zpl_url": "https://chitchats.com/labels/shipments/r94dt3f7dk.zpl"
  }
]
```

###### Copy as cURL
```shell
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

The `tracking_details` key contains an array of the tracking events for the shipment.

The `rates` key contains an array of the elgible postage rates for the shipment.

###### Example JSON Response
```json
{
  "shipment": {
    "id": "8ERNJ8SCQ9",
    "status": "received",
    "batch_id": 2,
    "to_name": "Tommy Lawrence",
    "to_address_1": "555 ELM RD, APT 17",
    "to_address_2": null,
    "to_city": "ROCHESTER",
    "to_province_code": "WA",
    "to_postal_code": "14623",
    "to_country_code": "US",
    "to_phone": null,
    "return_name": "AMISTAD NATIONAL RECREATION AREA",
    "return_address_1": "4121 VETERANS BLVD",
    "return_address_2": null,
    "return_city": "DEL RIO",
    "return_province_code": "TX",
    "return_postal_code": "78840-3384",
    "return_country_code": "US",
    "return_phone": "1-844-842-8777",
    "package_contents": "merchandise",
    "description": "Statue and documents in crate",
    "value": "20.00",
    "value_currency": "USD",
    "order_id": null,
    "order_store": null,
    "package_type": "parcel",
    "size_unit": "cm",
    "size_x": 28.0,
    "size_y": 21.0,
    "size_z": 21.0,
    "weight_unit": "g",
    "weight": 1850.0,
    "is_insured": false,
    "is_signature_requested": false,
    "postage_type": "usps_priority",
    "carrier": "usps",
    "carrier_tracking_code": "9405536895357112578988",
    "tracking_url": "https://chitchats.com/tracking/8ernj8scq9",
    "ship_date": "2017-11-15",
    "purchase_amount": "22.39",
    "provincial_tax": null,
    "provincial_tax_label": null,
    "federal_tax": null,
    "federal_tax_label": null,
    "postage_fee": "22.39",
    "insurance_fee": null,
    "delivery_fee": "1.00",
    "created_at": "2017-11-14T11:04:32.168-08:00",
    "postage_label_png_url": "https://chitchats.com/labels/shipments/8ernj8scq9.png",
    "postage_label_zpl_url": "https://chitchats.com/labels/shipments/8ernj8scq9.zpl",
    "rates": [
      {
        "postage_type": "ups_mi_expedited",
        "postage_carrier_type": "ups_mi",
        "postage_description": "UPS Mail Innovations Parcel Select",
        "signature_confirmation_description": null,
        "delivery_time_description": "2-9 business days",
        "tracking_type_description": "Full tracking included",
        "is_insured": true,
        "purchase_amount": "4.23",
        "provincial_tax": null,
        "provincial_tax_label": null,
        "federal_tax": null,
        "federal_tax_label": null,
        "postage_fee": "4.23",
        "insurance_fee": "0.35",
        "delivery_fee": "0.85",
        "payment_amount": "5.43"
      },
      {
        "postage_type": "usps_first",
        "postage_carrier_type": "usps",
        "postage_description": "USPS First-Class Mail®",
        "signature_confirmation_description": null,
        "delivery_time_description": "2-4 business days",
        "tracking_type_description": "Full tracking included",
        "is_insured": true,
        "purchase_amount": "4.28",
        "provincial_tax": null,
        "provincial_tax_label": null,
        "federal_tax": null,
        "federal_tax_label": null,
        "postage_fee": "4.28",
        "insurance_fee": "0.35",
        "delivery_fee": "0.85",
        "payment_amount": "5.48"
      }
    ],
    "tracking_events": [
      {
        "type": "receive_shipment",
        "title": "Received by Chit Chats",
        "subtitle": "Delivery Fee $1.00",
        "location_description": null,
        "created_at": "2017-11-15T09:53:32.991-08:00",
        "status": null
      },
      {
        "type": "buy_shipment_postage",
        "title": "Postage purchased",
        "subtitle": "USPS Priority Mail® $22.39",
        "location_description": null,
        "created_at": "2017-11-15T09:45:42.841-08:00",
        "status": null
      },
      {
        "type": "create_shipment",
        "title": "Shipment created",
        "subtitle": null,
        "location_description": null,
        "created_at": "2017-11-14T11:04:32.177-08:00",
        "status": null
      }
    ]
  }
}
```

###### Copy as cURL
```shell
curl -H "Authorization: $ACCESS_TOKEN" \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/shipments/1by4s9h87b"
```


Create a shipment
-----------------

* `POST /shipments` with the required parameters (see example) to create a new shipment.

_Enumeration values_:

* `package_contents`:
  * `merchandise` - Merchandise
  * `documents` - Documents
  * `gift` - Gift
  * `returned_goods` - Returned goods
  * `sample` - Sample
  * `other` - Other
* `package_type`
  * `unknown` - Unknown
  * `card` - Postcard
  * `letter` - Letter
  * `envelope` - Flat Envelope
  * `thick_envelope` - Thick Envelope
  * `parcel` - Parcel
  * `flat_rate_envelope` - USPS Letter Flat Rate Envelope
  * `flat_rate_legal_envelope` - USPS Legal Flat Rate Envelope
  * `flat_rate_padded_envelope` - USPS Padded Flat Rate Envelope
  * `flat_rate_gift_card_envelope` - USPS Gift Card Flat Rate Envelope
  * `flat_rate_window_envelope` - USPS Window Flat Rate Envelope
  * `flat_rate_cardboard_envelope` - USPS Cardboard Flat Rate Envelope
  * `small_flat_rate_envelope` - USPS Small Flat Rate Envelope
  * `small_flat_rate_box` - USPS Small Flat Rate Box
  * `medium_flat_rate_box_1` - USPS Medium Flat Rate Box - 1
  * `medium_flat_rate_box_2` - USPS Medium Flat Rate Box - 2
  * `large_flat_rate_box` - USPS Large Flat Rate Box
  * `large_flat_rate_board_game_box` - USPS Large Flat Rate Board Game Box
  * `regional_rate_box_a_1` - USPS Priority Mail Regional Rate Box - A1
  * `regional_rate_box_a_2` - USPS Priority Mail Regional Rate Box - A2
  * `regional_rate_box_b_1` - USPS Priority Mail Regional Rate Box - B1
  * `regional_rate_box_b_2` - USPS Priority Mail Regional Rate Box - B2
* `postage_type`
  * `unknown` - Use when you wish to view rates before buying postage
  * `usps_express` - USPS Priority Mail Express®
  * `usps_express_mail_international` - USPS Priority Mail Express International®
  * `usps_first` - USPS First-Class Mail®
  * `usps_first_class_mail_international` - USPS First-Class Mail International
  * `usps_first_class_package_international_service` - USPS First-Class Package International Service®
  * `usps_library_mail` - USPS Library Mail
  * `usps_media_mail` - USPS Media Mail®
  * `usps_parcel_select` - USPS Parcel Select®
  * `usps_priority` - USPS Priority Mail®
  * `usps_priority_mail_international` - USPS Priority Mail International®
  * `usps_other` - USPS Other Mail Class
  * `ups_other` - UPS Other Mail Class
  * `fedex_other` - FedEx Other Mail Class
  * `chit_chats_canada_tracked` - Chit Chats Canada Tracked
  * `chit_chats_international_not_tracked` - Chit Chats International Standard
  * `chit_chats_us_tracked` - Chit Chats U.S. Tracked
  * `dhl_other` - DHL Other Mail Class
  * `asendia_priority_tracked` - Asendia International Priority Tracked
  * `ups_mi_expedited` - UPS Mail Innovations Parcel Select
* `size_unit`
  * `m` - Metres
  * `cm` - Centimetres
  * `in` - Inches
* `weight_unit`
  * `lb` - Pounds
  * `oz` - Ounces
  * `kg` - Kilograms
  * `g` - Grams
* `value_currency`:
  * `cad` - Canadian Dollar
  * `usd` - US Dollar

###### Example JSON Request
```json
{
  "name": "Jane Doe",
  "address_1": "123 ANYWHERE ST.",
  "address_2": "",
  "city": "Vancouver",
  "province_code": "BC",
  "postal_code": "V6K 1A1",
  "country_code": "CA",
  "phone": "800-555-1212",
  "package_contents": "merchandise",
  "description": "Hand made bracelet",
  "value": "84.99",
  "value_currency": "usd",
  "order_id": "",
  "order_store": "",
  "package_type": "parcel",
  "weight_unit": "g",
  "weight": 250,
  "size_unit": "cm",
  "size_x": 10,
  "size_y": 5,
  "size_z": 2,
  "insurance_requested": true,
  "signature_requested": false,
  "postage_type": "chit_chats_canada_tracked",
  "tracking_number": "",
  "ship_date": "today"
}
```

This will return `201 Created` with the URL of the shipment in the `Location` header and the created shipment in the response if the creation was a success. See the [Get a shipment](#get-a-shipment) endpoint for more info.

###### Copy as cURL
```shell
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
    "value": "84.99",
    "value_currency": "usd",
    "package_type": "parcel",
    "size_unit": "cm",
    "size_x": 10,
    "size_y": 5,
    "size_z": 2,
    "weight_unit": "g",
    "weight": 250,
    "postage_type": "chit_chats_canada_tracked",
    "ship_date": "today"
  }' \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/shipments"
```


Delete a shipment
-----------------

* `DELETE /shipments/abcde12345` will delete the pending shipment with the given ID if allowed. If the shipment has purchased postage or has been received by Chit Chats the shipment cannot be deleted but it can be refunded to void the shipment. No parameters required. Returns `204 No Content` if successful.

###### Copy as cURL

```shell
curl -s -X DELETE \
  -H "Authorization: $ACCESS_TOKEN" \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/shipments/abcde12345"
```

Refresh a shipment
------------------

* `PATCH /shipments/abcde12345/refresh` will refresh shipment and postage rates for the given shipment. Returns `200 OK` if successful.  A successful result will return the updated shipment.

The following parameters can be passed to update the shipment when refreshing.

* insurance_requested - `true` or `false`
* media_mail_requested - `true` or `false`
* signature_requested - `true` or `false`
* ship_date - Either `today` or a date in the format of `YYYY-MM-DD`

###### Copy as cURL
```shell
curl -s -X PATCH \
  -H "Authorization: $ACCESS_TOKEN" \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/shipments/abcde12345/refresh"
```

###### Copy as cURL
```shell
curl -X PATCH \
  -H "Authorization: $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "insurance_requested": true,
    "ship_date": "today"
  }' \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/shipments/abcde12345/refresh"
```

Buy shipment
------------

* `PATCH /shipments/abcde12345/buy` will attempt to buy the selected postage for the given shipment. Returns `200 OK` if successful.  A successful result only means that a purchase is requested.  The status of the shipment may be `postage_requested`.  If this happens the caller will need to wait a few seconds and poll until the shipment returns `ready` or `postage_purchase_failed`.

You can optionally pass the `postage_type` to select the rate.  Refer to the postage_types values returned by the `rates` array in the shipment details.

The reason for not blocking is that buying postage can take a few seconds (exact duration is dependent on our postage providers but this will normally complete in less than 3 seconds).  Because of the delay waiting to return for each call, is inefficient when buying 1000s of shipments. In this case, we recommend calling the buy end point on all your endpoints and then poll at reasonable intervals until the shipment's status changes to `ready`.  The example below shows how to accomplish this.

```ruby
def buy
  patch(:buy)

  # Buying postage can take a few seconds to process and generate a label
  # so block and poll until we know it doesn't fail.
  sleep(0.5) while reload.status == "postage_requested"
  raise "Purchase postage failed" if status == "postage_purchase_failed"

  status
end
```

###### Copy as cURL
```shell
curl -s -X PATCH \
  -H "Authorization: $ACCESS_TOKEN" \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/shipments/abcde12345/buy"
```

###### Copy as cURL
```shell
curl -X PATCH \
  -H "Authorization: $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"postage_type": "usps_first"}' \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/shipments/abcde12345/buy"
```


Refund shipment
---------------

* `PATCH /shipments/abced12345/refund` will request shipment refund for the given shipments if possible. Returns `200 OK` if successful.

###### Copy as cURL
```shell
curl -s -X PATCH \
  -H "Authorization: $ACCESS_TOKEN" \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/shipments/abcde12345/refund"
```


Add shipments to a batch
------------------------

* `PATCH /shipments/add_to_batch` will add the given shipments to the given batch. Returns `200 OK` if successful.

###### Example JSON Request
```json
{
  "batch_id": 1,
  "shipment_ids": [
    "ABCDE12345",
    "Q5P4R3S2T1"
  ]
}
```

###### Copy as cURL
```shell
curl -s -X PATCH \
  -H "Authorization: $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "batch_id": 1,
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
```json
{
  "shipment_ids": [
    "ABCDE12345",
    "Q5P4R3S2T1"
  ]
}
```

###### Copy as cURL
```shell
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
