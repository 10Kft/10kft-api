# Before starting to use the Resource Management by Smartsheet API

This documentation assumes that you have either signed up for a Resource Management by Smartsheet trial or you have an active subscription, and that you are familiar with the basic features of the application. The information that follows give you an overview of accessing the same functionality, from an API, so that you can implement additional functionality and custom integrations that meet your specific business needs.

We also assume that you are familiar with basic RESTful API concepts.

```
  IMPORTANT

  Do not perform stress or performance testing in any
  account without informing Resource Management by Smartsheet support and obtaining explicit
  approval. Violation of this may result in your account being suspended.
```

## Being notified about important changes

There are several ways in which you can stay informed about important changes to the API.

* Ask your friendly account Administrator to add your email as the developer contact for your account.
* Subscribe to be notified when updates are made to this github repo by following it or using the watch feature.

## Collections & Objects

The API follows a typical RESTful pattern where it allows you to access collections of objects via HTTP. These Collections are paginated, and are always delivered in a structure that has a 'data' array and 'paging' meta-data, as shown below. This is true top level as well as nested collections.

Some objects returned by the API may have sub-collections. For example, a tags collection for a given user object. These sub-collections are paginated in the same manner as top level collections.

```
curl -X GET https://api.rm.smartsheet.com/api/v1/users \
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
GET https://api.rm.smartsheet.com/api/v1/users?per_page=100&page=3
```

per_page should not exceed 1000 rows.

## Filtering

Some resources in the Resource Management by Smartsheet API respect certain filtering parameters. Those optional parameters are as follows:

- `filter_field` - The property to filter on.
- `filter_list` - The value of `filter_field` to match.

## Authentication

The API currently supports service token based authentication. This can be sent as a query parameter named `auth`, or as an HTTP header with the same name.

```
# Token in http header (recommended)
curl -X GET https://api.rm.smartsheet.com/api/v1/users \
  -H "Content-Type: application/json"
  -H "auth: TOKEN"

# Token on URL
curl -X GET https://api.rm.smartsheet.com/api/v1/users?auth=URL-ENCODED-TOKEN \
  -H "Content-Type: application/json"
```

Account administrators can obtain the API token from _Settings >_ _Developer API_ in the application.

## Optional Fields

To reduce the number of roundtrips that might be required to fetch all related data for a given collection or resource (e.g. fetching a user and all their tags), the API supports a concept of optional fields. These `fields` are a comma separated list of field names that are supported as a URL parameter when making a request to fetch a resource or a resource collection.

```
curl -X GET https://api.rm.smartsheet.com/api/v1/users?fields=tags \
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
      "tags": {
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

## Throttling & Rate-Limiting

The API throttles incoming requests to prevent abuse and ensure fair use.

When an application exceeds the rate limit, the API will return a standard HTTP `429 Too Many Requests` response.

### How to handle being throttled

The specific details of rate limit policies in effect may vary without notice. Application developers should implement detection and handling of rate-limiting behavior using `X-Ratelimit-*` headers described below.

When a request from your application receives a `429 Too many Requests` response, you can check the returned HTTP headers to see your current rate limit status:

```
X-RateLimit-Limit:120
X-RateLimit-Remaining:0
X-RateLimit-Reset:1482966442
```

The `X-RateLimit-Reset` provides the time at which the current rate limit window resets in UTC epoch seconds.

```
// pseudo-code

MAX_RETRIES = 25

retry_count = 0

while(running == true) {
  response = get_api_response(request_params)

  // if the server throttled the request, re-try until a valid
  // response is received or a maximum number of re-try attempts
  // have been reached
  //
  while(response.status == 429 && retry_count < MAX_RETRIES) {
    // extract the Time in X-RateLimit-Reset
    x_rate_limit_reset_time = get_x_rate_limit_reset(response)

    // wait until the rate limit time window has been reset
    wait_until(x_rate_limit_reset_time)

    // retry the call
    response = get_api_response(request_params)

    retry_count += 1
  }

  handle_response(response)

  retry_count = 0
}
```
