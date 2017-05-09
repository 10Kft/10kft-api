# Users

##### Endpoint: `/api/v1/users`

A user cannot be deleted by the API. A user can be archived by setting the optional parameter archived to true, it can also be unarchived by setting the optional parameter archived to false. You cannot archive the account owner.

## List Users (index)

##### Optional Parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| fields | A comma separated list of additional fields to include in the response [ "tags", "assignments", "availabilities", "custom_field_values" ] |
| per_page, page | Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first ) |
| with_archived | true to include deleted/archived users

```
GET  /api/v1/users
 curl 'https://vnext.10000ft.com/api/v1/users?fields=tags,assignments&auth=...'
```

## Show User

##### Optional Parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| fields | A comma separated list of additional fields to include in the response [ "tags", "assignments", "availabilities", "custom_field_values"] |
| per_page, page | Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first ) |

```
GET  /api/v1/users/<user_id>
 curl 'https://vnext.10000ft.com/api/v1/users/12345?fields=tags,assignments&auth=...'
```

## Create User

##### Required Parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| `email` | Desired email address for the user |
| `first_name` | User's first name |
| `last_name` | User's last name |

```
POST  /api/v1/users
 curl -d 'first_name=John&last_name=Smith&email=john@sample.com' \
             'https://vnext.10000ft.com/api/v1/users?auth=...'
```

## Update a User

User specified by `id`

##### Optional Parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| archive | true to archive/false to unarchive |

```
PUT  /api/v1/users/<user_id>
 curl -XPUT -d 'first_name=Bob' \
             'https://vnext.10000ft.com/api/v1/users/12345?auth=...'
```

## User Permission Levels

Information about a user's permission level is contained in the user_type_id property in the API response. This value is an integer that can be interpreted as follows:

| **user_type_id** | **Permission level** |
| ------------- | --------------- |
| 0 | None |
| 1 | Administrator |
| 2 | Project Manager |
| 3 | Team Member |
| 4 | Restricted Team Member |
| 5 | Contractor |
| 7 | Scheduler |

Values not included in this list are reserved for internal/future use. Setting the permission level via API is not supported, and can only be done through application UI.

## Sample Response

```
{
  "data": [
            {
               "id": 1,
               "account_owner": true,
               "billability_target": 100.0,
               "billable": true, "billrate": -1.0,
               "deleted": false,
               "deleted_at": null, # deprecated see archived_at
               "archived_at": null,
               "discipline": null,
               "display_name": "Mark van Tilburgh", # read only
               "email": "claes@example.com",
               "employee_number": null,
               "first_name": "Mark",
               "guid": "40195EEC-2E47-403D-9E48-5B99A25FD2F9",
               "hire_date": "2011-11-21",
               "invitation_pending": false,
               "last_name": "van Tilburgh",
               "location": null,
               "mobile_phone": null,
               "office_phone": null,
               "role": null,
               "termination_date": null,
               "thumbnail": "",
             }
          ],
  "paging": {
             "next": null,
             "page": 1,
             "per_page": 20,
             "previous": null,
             "self": "/api/v1/users?per_page=20&page=1"
           }
}
```
