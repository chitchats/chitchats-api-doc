The Chit Chats API
==================

Welcome to the Chit Chats API! If you're looking to integrate your application with Chit Chats or create your own application in concert with data inside of Chit Chats, you're in the right place. We're happy to have you!


Making a request
----------------

All URLs start with **`https://chitchats.com/api/v1/`**. URLs are HTTPS only.

To make a request for all the shipments on your account, use your client ID in the URL replacing the 999999 placeholder to form something like `https://chitchats.com/api/v1/clients/999999/shipments`. In cURL, it looks like this:

```shell
curl -H "Authorization: $ACCESS_TOKEN" \
  "https://chitchats.com/api/v1/clients/999999/shipments"
```

To create something, it's the same idea, but you also have to include the `Content-Type` header and the JSON data:

```shell
curl -X POST \
  -H "Authorization: $ACCESS_TOKEN" \
  -H 'Content-Type: application/json' \
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
  "https://chitchats.com/api/v1/clients/999999/shipments"
```

Throughout the Chit Chats API docs, we include "Copy as cURL" examples. To try the examples in your shell, copy your access token into your clipboard and run:

```shell
export ACCESS_TOKEN=PASTE_ACCESS_TOKEN_HERE
export CLIENT_ID=999999
```

Then you should be able to copy/paste any example from the docs. After pasting a cURL example, you can pipe it to a JSON pretty printer to make it more readable. Try [jsonpp](https://jmhodges.github.io/jsonpp/) or `json_pp` on OSX:

```shell
curl -s -H "Authorization: $ACCESS_TOKEN" "https://chitchats.com/api/v1/clients/$CLIENT_ID/shipments" | json_pp
```

Authentication
--------------

Before you can use the API you must first create an API access token. You do this from the Settings > Account section of the Chit Chats website. Treat the access tokens as passwords and do not share them or check them into source code repositories. Deleting an access token will immediately revoke access.

Once you have an access token you must pass it in the `Authorization` header with every request.


JSON only
---------

We use JSON for all API data. The style is no root element and snake\_case for object keys. This means that you have to send the `Content-Type` header `Content-Type: application/json; charset=utf-8` when you're POSTing or PUTing data into Chit Chats.

You'll receive a `415 Unsupported Media Type` response code if you don't include the `Content-Type` header or you try to use a URL suffix other than `.json`.


Pagination
----------

Most collection APIs paginate their results. The default is usually 100. The limit can be increased to 1000. Use the `limit` and `page` URL parameters to control pagination or the `count` endpoint to get the number of records in a collection.


Handling errors
---------------

If Chit Chats is having trouble, you might get a 5xx error. `500` means that the application is entirely down, but `502 Bad Gateway`, `503 Service Unavailable`, or `504 Gateway Timeout` errors are also possible. In all of these cases, it's your responsibility to retry your request later.


Rate limiting
-------------

You can perform up to 2000 requests per 5 minute period from the same IP address for the same account. If you exceed this limit, you'll get a [429 Too Many Requests](http://tools.ietf.org/html/draft-nottingham-http-new-status-02#section-4) response for subsequent requests. Check the `Retry-After` header to learn how many seconds to wait before retrying the request.

We recommend baking 429 response-handling in to your HTTP handling at a low level so your integration handles retries gracefully and automatically.

API endpoints
-------------
- [Batches](https://github.com/chitchats/chitchats-api-doc/blob/master/sections/batches.md)
- [Shipments](https://github.com/chitchats/chitchats-api-doc/blob/master/sections/shipments.md)

Conduct
-------

Please note that this project is released with a [Contributor Code of Conduct](https://github.com/chitchats/chitchats-api-doc/blob/master/CONDUCT.md). By participating in discussions about the Chit Chats API, you agree to abide by these terms.


License
-------

These API docs are licensed under [Creative Commons (CC BY-SA 4.0)](http://creativecommons.org/licenses/by-sa/4.0/). Please share, remix, and distribute as you see fit.

Thanks to [Basecamp](https://github.com/basecamp/bc3-api) for providing a starting point for documenting an API.

---

If you have a specific feature request or find a bug, [please open a GitHub issue](https://github.com/chitchats/chitchats-api-doc/issues/new). We encourage you to fork these docs for local reference and happily accept pull requests with improvements.

To talk with us and other developers about the API, [post a question on StackOverflow](http://stackoverflow.com/questions/ask) tagged `chitchats`. If you need help from us directly, please [open a support ticket](https://support.chitchats.com).
