# 10Kft API

The 10Kft API provides programmatic access to projects, users and time entries in your account, commonly referred to as _resources_ in the rest of this API documentation. The API implements a standard HTTP REST pattern and allows callers with appropriate authentication and authorization to programmatically create, read, update and delete these resources.

This documentation assumes that you have either signed up for a 10Kft trial or you have an active subscription, and that you are familiar with the basic features of the application. The information that follows give you an overview of accessing the same functionality, from an API, so that you can implement additional functionality and custom integrations that meet your specific business needs.

We also assume that you are familiar with basic RESTful API concepts.

### Being notified about important changes

There are several ways in which you can stay informed about important changes to the API.

* Ask your friendly 10Kft Administrator to add your email as the developer contact for your account.
* Subscribe to be notified when updates are made to this github repo by following it or using the watch feature.
* Sign up to receive updates via the 10Kft Developer API Announcements mailing list [here](http://eepurl.com/ZvuOb)

### Getting help & reporting problems

There are several ways you can ask for help with using the API.

* For issues that require immediate attention, contact us via the support widget within the 10Kft Plans app, or email support@10000ft.com
* For suggestions of feature requests and other non urgent issues, [open an issue](https://github.com/10Kft/10kft-api/issues) in this repo.

When contacting support for assistance with using the API, please provide example API calls where possible. This greatly speeds up the time to resolve support requests. You can use cURL, available on unix platforms as well as windows, to create an example of your scenario, and including the `curl` command(s) along with your request for support.

Here are some example `curl` commands;

```
# get the collection of users
curl -X GET https://api.10000ft.com/api/v1/users?auth=TOKEN \
  -H "Content-Type: application/json"

# update user 100 with a new last_name
curl -X PUT https://api.10000ft.com/api/v1/users/100?auth=TOKEN \
  -H "Content-Type: application/json" \
  -d '{"last_name":"Silva"'}'
```

### Staging vs. Production Environments

We provide a development environment called **`vnext`** so your can test out the API and develop your applications before going live with them in production. It is a staging environment completely isolated from our active account. We strongly encourage that you setup a test account on `vnext` and build your integrations there before moving to production.

There is no additional charge for maintaining a test account on vnext.

### How do I access the staging environment?

* Visit [`https://vnext.10000ft.com/signup`](https://vnext.10000ft.com/signup) to setup a test account.
* The API end point base URL for `vnext` is `https://vnext-api.10000ft.com/api/v1/`
* To access your test account, visit `https://vnext.10000ft.com` and sign in with your test account credentials.
* For support on vnext integration, contact us via email at `support@10000ft.com`

### What changes when moving my integration to production?

* Your production account is your live 10,000ft Plans account available at `https://app.10000ft.com`
* The API end point base URL is `https://api.10000ft.com/api/v1/`
* You will use a production API token obtained from the settings section in your production account.

# Endpoints

The API provides access to the following data collections available in your account.

* [Users](sections/users.md)
  * [User Tags](sections/user-tags.md)
  * [Statuses](sections/user-statuses.md)
* [Projects](sections/projects.md)
  * [Users by Project](sections/project-users.md)
  * [Project Tags](sections/project-tags.md)
  * [Bill Rates](sections/bill-rates.md)
  * [Phases](sections/phases.md)
* [Time Entries](sections/time-entries.md)
* [Assignments](sections/assignments.md)

### Pro & Enterprise Only Endpoints

* Approvals (_coming soon_)
* Custom Fields (_coming soon_)

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

> `NB:` A separate token is issues each time an Administrator visits the Developer API section under settings. This however does not invalidate the current token in use for your application.

## Optional Fields

To reduce the number of roundtrips that might be required to fetch all related data for a given collection or resource (e.g. fetching a user and all their tags), the API support a concept of optional fields. These `fields` are a comma separated list of field names that are supported as a URL parameter when making a request to fetch a resource or a resource collection.

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

## Questions?

Please don't hesitate to reach out to us via the in app support feature for questions or suggestions about using the 10Kft API. We're here to help.
