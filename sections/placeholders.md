# Placeholder Resources

##### Endpoint: `/api/v1/placeholder_resources`

Placeholder resources can be used for temporary resourcing on projects where the final resources are not yet known. Placeholders behave quite similarly to users, with a few differences discussed below.

## List Placeholder Resources (index)

##### Optional Parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| fields | A comma separated list of additional fields to include in the response [ "assignments", "custom_field_values"] |
| per_page, page | Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first ) |

```
GET  /api/v1/placeholder_resources
 curl 'https://vnext.10000ft.com/api/v1/placeholder_resources?fields=assignments,custom_field_values&auth=...'
```

Note that custom field values can only be accessed if custom fields are enabled for the account. This is only possible for pro plans and up. See [custom fields](sections/custom fields.md) for details. 

## Show Placeholder

##### Optional Parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| fields | A comma separated list of additional fields to include in the response [ "assignments", "custom_field_values"] |
| per_page, page | Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first ) |

```
GET  /api/v1/placeholder_resources/<placeholder_resource_id>
 curl 'https://vnext.10000ft.com/api/v1/placeholder_resources/12345?fields=assignments&auth=...'
```

## Create a Placeholder Resource

##### Required Parameters

| `title` |

```
POST  /api/v1/placeholder_resources
 curl -d 'title=Designer' \
             'https://vnext.10000ft.com/api/v1/placeholder_resources?auth=...'
```

Placeholders are referred to by title. The title is displayed wherever placeholders appear in the application e.g. on projects, the schedule, etc. Therefore, it is required to specify this parameter.

## Update a User

User specified by `id`

```
PUT  /api/v1/users/<user_id>
 curl -XPUT -d 'first_name=Bob' \
             'https://vnext.10000ft.com/api/v1/users/12345?auth=...'
```

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
