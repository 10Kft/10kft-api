# Getting help & reporting problems

There are several ways you can ask for help or report a problem with using the API.

* For issues that require immediate attention, contact us via our [Support Page](https://help.smartsheet.com/contact/resource-management)

When contacting support for assistance with using the API, please provide example API calls where possible. This greatly speeds up the time to resolve support requests. You can use cURL, available on unix platforms as well as windows, to create an example of your scenario, and including the `curl` command(s) along with your request for support.

Here are some example `curl` commands;

```
# get the collection of users
curl -X GET https://api.rm.smartsheet.com/api/v1/users?auth=TOKEN \
  -H "Content-Type: application/json"

# update user 100 with a new last_name
curl -X PUT https://api.rm.smartsheet.com/api/v1/users/100?auth=TOKEN \
  -H "Content-Type: application/json" \
  -d '{"last_name":"Silva"'}'
```
