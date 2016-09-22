# Time Entries by Project

##### Endpoint: `/api/v1/projects/<project_id>/time_entries`

Time Entries is a collection of hours reported for a user on a project. 

## List Time Entries for a Project

##### Optional parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| from | filter on date, i.e. formatted as YYYY-MM-DD or DD/MM/YYYY |
| to | filter on date, i.e. formatted as YYYY-MM-DD or DD/MM/YYYY |
| with_suggestions | true/false, to include suggested time entries |
| per_page, page | Parameters for pagination.Default values are per_page = 20 , page = 1 ( the first ) |

```
GET /api/v1/projects/<project_id>/time_entries
     curl 'https://vnext.10000ft.com/api/v1/projects/4/time_entries?auth=..'
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
            "date": "2013-09-12",
            "hours": 8.0,
            "id": 2,
            "is_suggestion": false,
            "notes": null,
            "scheduled_hours": null,
            "task": null,
            "updated_at": "2013-09-12T04:32:28Z"
            "user_id": 1
        }
    ],
    "paging": {
        "next": null,
        "page": 1,
        "per_page": 20,
        "previous": null,
        "self": "/api/v1/projects/4/time_entries?project_id=4&per_page=20&page=1"
    }
 }
```
