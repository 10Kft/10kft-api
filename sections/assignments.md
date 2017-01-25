# Assignments

##### Endpoint: `/api/v1/users/<user_id>/assignments`
##### Endpoint: `/api/v1/projects/<project_id>/assignments`

Assignments connect a [User](users.md) to a [Project](projects.md) or a [Phase](phases.md) (part of a project) or a [LeaveType](leave-types).

## List assignments for a User or Project

##### Optional parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| from |  get assignments that start on or after this date |
| to |  get assignments that end on or before this date |
| per_page, page |  Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first ) |

```
GET /api/v1/users/<user_id>/assignments

 curl 'https://vnext.10000ft.com/api/v1/users/1/assignments?auth=..'
```

```
GET /api/v1/projects/<project_id>/assignments

 curl 'https://vnext.10000ft.com/api/v1/projects/1/assignments?auth=..'
```

## Show an Assignment for a User or Project

```
GET /api/v1/users/<user_id>/assignments/<assignment_id>

 curl 'https://vnext.10000ft.com/api/v1/users/1/assignments/456?auth=..'
```

```
GET /api/v1/projects/project_id/assignments/<assignment_id>

 curl 'https://vnext.10000ft.com/api/v1/projects/1/assignments/456?auth=..'
```

Similarly, in the create and delete examples below, you can all the assignments API on projects specifying a user_id to create an assignment for that user, or to delete an assignment.

## Create an Assignment

Typical parameters: `starts_at`, `ends_at`, `percent`, `fixed_hours`

```
POST /api/v1/users/<user_id>/assignments

 curl -d 'leave_id=1&starts_at=2013-10-10&ends_at=2013-10-15'  \
                 'https://vnext.10000ft.com/api/v1/users/1/assignments?auth=...'

 curl -d 'leave_id=1&starts_at=2013-10-10&ends_at=2013-10-15&percent=0.25'  \
                 'https://vnext.10000ft.com/api/v1/users/1/assignments?auth=...'
```

## Remove an Assignment for a User

```
DELETE /api/v1/users/<user_id>/assignments/<assignment_id>

 curl -XDELETE 'https://vnext.10000ft.com/api/v1/users/1/assignments/456?auth=...'
```

## Sample Response

```
{
    "data": [
        {
            "id":889,
            "allocation_mode":"percent",
            "percent":1.0 /* only present when allocation_mode is percent */,
            "hours_per_day":8 /* only present when allocation_mode is hours_per_day */,
            "fixed_hours":8 /* only present when allocation_mode is fixed */,
            "user_id":5612,
            "assignable_id":123,
            "ends_at":"2013-10-07",
            "starts_at":"2013-10-03",
            "bill_rate":1.0,
            "bill_rate_id":0
            "repetition_id:" 886,
        },
        ...
    ],
    "paging": {
        "next": null,
        "page": 1,
        "per_page": 20,
        "previous": null,
        "self": "/api/v1/users/1/assignments?user_id=1&per_page=20&page=1"
    }
}
```

**Notes**: `repeition_id` is used for repeated assignments. The value will be NULL when the assignment is not part or a repeating series. `repeition_id` is equal to the parent assignment.
