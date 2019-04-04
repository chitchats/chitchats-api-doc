Tracking
=========

You can get public tracking events as JSON from any recent Chit Chats shipment ID by adding a `.json` suffix to the public tracking URL.

E.g., if the Chit Chats shipment ID was B5T85U7E1C you can get the public
tracking page at:  
https://chitchats.com/tracking/b5t85u7e1c

and the JSON tracking page at:  
https://chitchats.com/tracking/b5t85u7e1c.json


###### Copy as cURL
```shell
curl -s "https://chitchats.com/tracking/b5t85u7e1c.json"
```

###### Example JSON Request
```json
{
  shipment: {
    shipment_id: "B5T85U7E1C",
    to_city: "DEL RIO",
    to_province_code: "TX",
    to_postal_code: "78840-3384",
    to_country_code: "US",
    from_city: null,
    from_province_code: null,
    from_postal_code: null,
    from_country_code: null,
    package_description: "Parcel",
    size_description: "1 × 1 × 1 cm",
    weight_description: "0.3 lb",
    resolution: "unknown",
    postage_description: "Unknown Unknown",
    estimated_delivery_at: null,
    carrier: "unknown",
    carrier_description: "Unknown",
    carrier_tracking_code: null,
    tracking_url: "https://chitchats.com/tracking/b5t85u7e1c",
    ship_date: "2019-02-18",
    resolution_description: "Expected Delivery",
    resolved_at: null,
    tracking_events: [
      {
      title: "Shipment created, Chit Chats awaiting item",
      subtitle: null,
      location_description: null,
      created_at: "2019-01-26T17:28:59.797-08:00",
      status: null
      }
    ]
  }
}
```
