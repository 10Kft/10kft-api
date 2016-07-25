# Time Entries by User

##### Endpoint: `/api/v1/users/<user_id>/time_entries`

Time Entries are a collection of hours reported by a user on a project or leave type.

## Time Entries and Permissions

You can enter and confirm time for active users via the API, however this excludes Resource Only and Invitation-Pending users. Timesheets for Resource Only and Invitation-Pending users are read-only for all permission levels, and not editable via the API.

## List Time Entries for a User

##### Optional parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| from | get projects that start on or after this date |
| to | get projects that end on or before this date |
| with_suggestions | true to include suggested time entries based on assignments on the schedule |
| per_page, page | Parameters for pagination.Default values are per_page = 20 , page = 1 ( the first ) |

```
GET /api/v1/users/<user_id>/time_entries
 curl 'https://vnext.10000ft.com/api/v1/users/1/time_entries?auth=..'
```

## Show a Time Entry For a User

```
GET /api/v1/users/<user_id>/time_entries/<time_entry_id>
 curl 'https://vnext.10000ft.com/api/v1/users/1/time_entries/456?auth=..'
```

## Create Time Entry

When creating time entries, at least date and hours needs to be specified. Project/Leave Type can be specified by one of `project_id`, `leave_type_id`, or an `assignable_id`. These three parameters refer to the same and are interchangeable. You should only specify one of these parameters per time entry call.

| `date` | `hours` | `leave_type_id` | `project_id` | `assignable_id` |

```
POST /api/v1/users/<user_id>/time_entries
 curl -d 'leave_id=1&date=2013-10-10&hours=8'  \
                 'https://vnext.10000ft.com/api/v1/users/1/time_entries?auth=..'
 alt.
 curl -d 'date=2013-10-15&hours=5'  \
                 'https://vnext.10000ft.com/api/v1/projects/987/users/1/time_entries?auth=..'
```

## Update a Time Entry

```
PUT  /api/v1/projects/users/time_entries/
  curl  -XPUT -d "hours=3"  "https://vnext.10000ft.com/api/v1/projects/5/users/7/time_entries/12345?auth=..."
```

## Delete a Time Entry

```
  DELETE  /api/v1/users/users/time_entries/
  curl  -XDELETE  "https://vnext.10000ft.com/api/v1/projects/5/users/7/time_entries/12345?auth=..."
```

## Sample Response

```
{
    "data": [
        {
            "assignable_id": 4,
            "assignable_type": "Project",
            "bill_rate": 150,
            "bill_rate_id": 4,
            "created_at": "2013-09-12T04:32:28Z",
            "date": "2013-09-11",
            "hours": 8.0,
            "id": 3,
            "is_suggestion": false,
            "notes": null,
            "scheduled_hours": null,
            "task": null,
            "updated_at": "2013-09-18T04:32:28Z"
            "user_id": 1
        }
    ],
    "paging": {
        "next": null,
        "page": 1,
        "per_page": 20,
        "previous": null,
        "self": "/api/v1/users/1/time_entries?user_id=1&per_page=20&page=1"
    }
}
```
