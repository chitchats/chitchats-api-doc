Batches
=======

Endpoints:

- [Get all batches](#get-batches)
- [Count batches](#count-batches)
- [Get a batch](#get-a-batch)
- [Create a batch](#create-a-batch)
- [Delete a batch](#delete-a-batch)


Get all batches
----------------

* `GET /batches` will return a [paginated list][pagination] of active batches belong to the client sorted by most recently created batch first.

_Optional parameters_:

* `limit` (integer) - number of records to return per page (default is 100)

* `page` (integer) - pagination page number (default is 1)

* `state` (enum) - allows for searching batches based on the following states:
  * `pending` - batches that have not been received.
  * `ready` - batches that have not been received but with all shipments ready to receive.
  * `received` - batches that have been received.

* `to_date` (date) - when set, only return shipments with a `created_at` greater than or equal to the given date.

###### Example JSON Response
```json
[
  {
    "id": 2,
    "status": "received",
    "created_at": "2017-09-11T17:32:35.691-07:00"
  },
  {
    "id": 1,
    "status": "received",
    "created_at": "2017-09-11T17:29:21.912-07:00"
  }
]
```

###### Copy as cURL
```shell
curl -s -H "Authorization: $ACCESS_TOKEN" \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/batches"
```


Count batches
---------------

* `GET /batches/count` will return number of batches. You can pass the `state` parameter in [Get all shipments](#get-all-shipments) to count shipments in a specific state.

###### Example JSON Response
```json
{
  "count": 2
}
```


Get a batch
-----------

* `GET /batches/1` will return the batch with the given ID.

###### Example JSON Response
```json
{
  "id": 1,
  "status": "received",
  "created_at": "2017-09-11T17:29:21.912-07:00"
}
```

###### Copy as cURL

``` shell
curl -s -H "Authorization: $ACCESS_TOKEN" \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/batches/1"
```


Create a batch
--------------

* `POST /batches` to create a new batch.

###### Example JSON Request

This will return `201 Created` if the creation was a success with the URL of batch in the `Location` header. See the [Get a batch](#get-a-batch) endpoint for more info.

###### Copy as cURL

``` shell
curl -s -X POST \
  -H "Authorization: $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/batches"
```


Delete a batch
--------------

* `DELETE /batches/1` will delete the batch with the given ID if it is empty. Returns `204 No Content` if successful.

###### Copy as cURL

``` shell
curl -s -X DELETE \
  -H "Authorization: $ACCESS_TOKEN" \
  "https://chitchats.com/api/v1/clients/$CLIENT_ID/batches/1"
```


[pagination]: https://github.com/chitchats/chitchats-api-doc/blob/master/README.md#pagination
