# 10Kft API

The 10Kft API provides programmatic access to projects, users and time entries in your account, commonly referred to as resources in the rest of this document. The API implements a standard HTTP REST pattern and allows callers with appropriate authentication and authorization to programmatically create, read, update and delete these resources.

## Overview

### How can I stay informed about upcoming API updates?

If you are integrating with the 10Kft API or plan to do so, you can sign up for announcements that may impact you. 

* Ask one of your friendly 10Kft account adminstrators add your email as a developer contact.
* Sign up to recieve updates via the 10Kft Developer API Announcements mailing list [here](http://eepurl.com/ZvuOb)
* Watch or follow this github repo.

### Reporting problems with the API?

There are two ways you can do that.

* For issues that require immediate attention, contact us via the support widget within the 10Kft Plans app, or email support@10000ft.com
* For suggestions of feature requests and other non urgent issues, open an issue in this github repo.

When contacting support for assistance with using the API, please provide example API calls where possible. This greatly speeds up the time to resolve support requests. You can use cURL, available on unix platforms as well as windows, to create an example of your scenario, and including the curl command(s) along with your request for support.

Here are some example curl commands;

```sh
# get the collection of users
curl -H "Content-Type: application/json" -X GET https://api.10000ft.com/api/v1/users?auth=TOKEN

# update user 100 with a new last_name
curl -H "Content-Type: application/json" -X PUT -d '{"last_name":"Silva"' https://api.10000ft.com/api/v1/users/100?auth=TOKEN
```

### Test vs. Production Environments

We provide a staging/test environment which we call **`vnext`**. It is a staging environment fully isolated from our production environment. We strongly encourage you setup a test account there and test your integrations before moving to production. Test accounts on `vnext` are separate from your production accounts, and give you full isolation as far as your account data is concerned. 

There is no additional charge for maintaining a test account.

### How do I access the staging environment?

* Visit [`https://vnext.10000ft.com/signup`](https://vnext.10000ft.com/signup) to setup a test account. 
* The API end point base URL for `vnext` is `https://vnext-api.10000ft.com/api/v1/`
* To access your test account, visit `https://vnext.10000ft.com` and sign in with your test account credentials.
* For support on vnext integration, contact us via email at `support@10000ft.com`

### What changes when moving my integration to production?

* Your production account is your live 10,000ft Plans account available at `https://app.10000ft.com`
* The API end point base URL is `https://api.10000ft.com/api/v1/`
* You will use a production API token obtained from the settings section in your production account.

## Data Collections

The API provides access to the following data collections available in your account.

* [Users](sections/users.md)
  * [User Tags](sections/user-tags.md)
  * [Statuses](sections/user-statuses.md)
* [Projects](sections/projects.md)
  * [Users by Project](sections/project-users.md)
  * [Project Tags](setions/project-tags.md)
  * [Bill Rates](sections/bill-rates-project.md)
* [Phases](sections/phases.md)
* [Time Entries](sections/time-entries.md)
* [Assignments](sections/assignments.md)
* [Tags](sections/tags.md)

## Collections and Objects

The API, in typical RESTful fashion, lets you access collections of objects. These Collections are paginated, and are always delivered in a structure that has a 'data' array and 'paging' meta-data, as shown below. This is true top level as well as nested collections.

Some objects returned by the API may have sub-collections. For example, a tags collection for a given user object. These sub-collections are paginated in the same manner as top level collections.

## Authentication

The API expects an API authentication token (api-token) to be passed in with every API request. This can be sent as a query parameter named `auth`, or as an HTTP header with the same name.

Account administrators can find the API key under _Settings >_ _Developer API_. Note that you will get separate API tokens for development/test purposes vs final integration with your account on 10000ft.com.

## Pagination

The pagination section in collections provide mechanisms to fetch additional data. The `previous` and `next` links provide access to the corresponding pages in the collection.

You can override the default `per_page` value by providing an appropriate value in the URL query parameter. For example,

```
GET /api/v1/users?per_page=100
```

## Date Formatting

The API handles or expects dates and datetime values in various scenarios, and expects the values to be in specific formats.

Date values provided as query parameters when making API calls must be in the `YYYY-MM-DD` format or `DD/MM/YYYY` format.

## Error Handling

Respond with standard HTTP error messages, with 4XX codes to indicate client (caller) errors. There may be an optional response body with a message that has details for debugging / error logging. This message is not meant to end user display or consumption.

```
HTTP/1.1 400 Bad Request
{ "message" : "The request body had invalid json" }
```

## Throttling & Limits

Coming Soon.

# Examples

## Fetching a Collection

```
GET /api/v1/users

response:
{
  "data" : [
    { "id" : 1, "first_name" : "claes", ... },
     ...
  ],
  "paging": {
    "next": null,
    "page": 1,
    "per_page": 20,
    "previous": null,
    "self": "/api/v1/users/1/statuses?user_id=1&per_page=20&page=1"
  }
}
```

## Fetching an Object

```
GET /api/v1/users/5

response:
{
  "id" : 5,
  "first_name" : "claes",
  ...
}
```

## Fetching an Object With Optional Fields

```
GET /api/v1/users/5?fields=tags

response:
{
  "id" : 5,
  "first_name" : "claes",
  ...,
  "tags" : {
    "data" : [ "developer", "seattle", ... ],
    "paging" : { ... }
  }
}
```

## Updating an Object

```
PUT /api/v1/users/5

{
  "id" : 5,
  "first_name" : "Claes"
}
response:
{
  "id" : 5,
  "first_name" : "Claes",
  ...
}
```

## Creating an Object

```
POST /api/v1/users

{
  "first_name" : "Nick"
  "first_name" : "Pants"
}

response:
{
  "id" : 6,
  "first_name" : "Nick",
  ...
}
```

## Deleting an Object

```
DELETE /api/v1/users/5
```
