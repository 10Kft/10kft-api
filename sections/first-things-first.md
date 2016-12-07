# Before starting to use the 10,000ft API

This documentation assumes that you have either signed up for a 10,000ft trial or you have an active subscription, and that you are familiar with the basic features of the application. The information that follows give you an overview of accessing the same functionality, from an API, so that you can implement additional functionality and custom integrations that meet your specific business needs.

We also assume that you are familiar with basic RESTful API concepts.

## Being notified about important changes

There are several ways in which you can stay informed about important changes to the API.

* Ask your friendly account Administrator to add your email as the developer contact for your account.
* Subscribe to be notified when updates are made to this github repo by following it or using the watch feature.
* Sign up to receive updates via the 10,000ft Developer API Announcements mailing list [here](http://eepurl.com/ZvuOb)

## Collections & Objects

The API follows a typical RESTful pattern where it allows you to access collections of objects via HTTP. These Collections are paginated, and are always delivered in a structure that has a 'data' array and 'paging' meta-data, as shown below. This is true top level as well as nested collections.

Some objects returned by the API may have sub-collections. For example, a tags collection for a given user object. These sub-collections are paginated in the same manner as top level collections.

```
curl -X GET https://api.10000ft.com/api/v1/users \
  -H "Content-Type: application/json"
  -H "auth: TOKEN"
```

Will get a JSON response like,

```
{
  "data" : [
    { "id" : 1, "first_name" : "Tom", "last_name" : "Perera" },
    { "id" : 2, "first_name" : "Jane", "last_name" : "Albert" },
    ...
  ],
  "paging": {
    "page": 1,
    "per_page": 20,
    "previous": null,
    "self": "/api/v1/users/1/statuses?user_id=1&per_page=20&page=1",
    "next": null
  }
}
```

Unless otherwise noted, the API always responds with **JSON**.

## Pagination

The pagination section in collections provide mechanisms to fetch additional data. The `previous` and `next` links provide access to the corresponding pages in the collection. You can override the default `per_page` value by providing an appropriate value in the URL query parameter. For example,

```
GET https://app.10000ft.com/api/v1/users?per_page=100&page=3
```

## Authentication

The API currently supports service token based authentication. This can be sent as a query parameter named `auth`, or as an HTTP header with the same name.

```
# Token in http header (recommended)
curl -X GET https://api.10000ft.com/api/v1/users \
  -H "Content-Type: application/json"
  -H "auth: TOKEN"

# Token on URL
curl -X GET https://api.10000ft.com/api/v1/users?auth=URL-ENCODED-TOKEN \
  -H "Content-Type: application/json"
```

Account administrators can obtain the API token from _Settings >_ _Developer API_ in the application.

> `NB:` A separate token is issued each time an Administrator visits the Developer API section under settings. This however does not invalidate the current token in use for your application.

## Optional Fields

To reduce the number of roundtrips that might be required to fetch all related data for a given collection or resource (e.g. fetching a user and all their tags), the API supports a concept of optional fields. These `fields` are a comma separated list of field names that are supported as a URL parameter when making a request to fetch a resource or a resource collection.

```
curl -X GET https://api.10000ft.com/api/v1/users?fields=tags \
  -H "Content-Type: application/json"
  -H "auth: TOKEN"

```

Each field requested is included in the response as nested collections. The page size for these nested collections will be the same as the page size used for the parent API request.

```
{
  "data" : [
    {
      "id" : 1,
      "first_name" : "Tom",
      "last_name" : "Perera",
      tags: {
        "data" : [
          { "id" : 1, "value" : "developer" },
          { "id" : 2, "value" : "javascript" },
        ],
        "paging" : {
          ...
        }
      }
    },
    ...
  ],
  "paging": {
    ...
  }
}
```

Multiple optional fields can be requested in a single API call like `fields=f1,f2`.

## Date & Time Formatting

The API handles or expects dates and date-time values in various scenarios, and expects the values to be in specific formats.

**Date** values provided as query parameters when making API calls must be in the `2013-01-31` format.

**Time** values are accepted in the `2013-09-31T22:10:24Z` format, which is a date and time value in UTC time.

## Error Handling

Respond with standard HTTP error messages, with 4XX codes to indicate client (caller) errors. There may be an optional response body with a message that has details for debugging / error logging. This message is not meant to end user display or consumption.

```
HTTP/1.1 400 Bad Request { "message" : "The request body had invalid json" }
```

## Throttling & Limits

The API currently throttles incoming requests to prevent abuse and ensure fair use. When throttling has been triggered, the affected callers will receive a HTTP response with status `429 Too Many Requests`.

### What to do when being throttled?

Our current recommendation is to implement a progressive back-off approach until your requests start processing normally. The psuedo-code below illustrate a simple scenario which you may adopt to suit your particular case.

```
// pseudo-code

DELAY = 100
MULTIPLIER = 1

MAX_RETRIES = 25

while(running == true) {
  response = get_api_response(url)

  // If hitting rate limit, re-try with progressive back off
  while(retry_count < MAX_RETRIES && response.status == 429) {
    retry_count += 1
    MULTIPLIER = MULTIPLIER * 2

    sleep(DELAY * MULTIPLIER)

    response = get_api_response(url)
  }

  handle_response(response)

  retry_count = 0
  MULTIPLIER = 1
}
```

The API does not expose `X-RateLimit` headers for clients to dynamically adjust their request rates.
