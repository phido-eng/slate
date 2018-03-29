---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam efficitur semper nisl dignissim congue. Pellentesque vel est at velit commodo finibus non et ex. Mauris eu aliquam ligula. Phasellus maximus accumsan rutrum. Fusce dictum lectus vitae ipsum fermentum, nec pharetra lorem pharetra. Donec tempor metus et nulla sodales viverra. Nunc convallis cursus hendrerit. Aenean sodales mollis eros, at consequat arcu varius eget. Duis auctor libero sit amet ex placerat, ac volutpat dolor malesuada. Quisque aliquet a sem a aliquam. Donec pellentesque vitae metus eget varius.

# Authentication

In order to authenticate with the API, you will need an API token. Eventually, we will have a UI allowing you to create/revoke tokens yourself, but until this functionality is complete, we will be handling the access tokens ourselves and passing them off on an individual basis.

To authenticate a request, simply add a bearer token header, like so:
<br />
<br />
```Authorization: {Bearer BearerToken}```

<aside class="notice">
You must replace <code>BearerToken</code> with your personal API key.
</aside>

# Pagination
Our API GET endpoints utilize pagination. You may pass limits (i.e: ?limit=20) and pages (i.e: ?page=2) on these endpoints.

# Security
Our API endpoints require use of a bearer token, as described in the above section. Bearer tokens are 1:1 with a retailer in our system. You will only be able to see/modify/create customer, order, and product data that is relevant to your own shop. Tokens must be kept secure, and if compromised, you will need to notify us so that we can revoke the token and re-issue you a new one.

# Orders

## Get orders

This endpoint provides general order searching functionality

> The orders JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

### HTTP Request

`GET http://example.com/api/orders`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
query | null | If an email address, will search for orders for a particular email address. If numeric, will attempt to lookup by EA internal order number. If is a string, attempts to look up by customer's last name.
per_page | 10 | Orders per page [see pagination section above](#pagination).
since | null | Orders created since this date. Format: m-d-Y. If format is wrong, is ignored.
status | null | Either `open` (PENDING or SCHEDULED) or `closed` (SHIPPED, CANCELED, or FAILED)

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

