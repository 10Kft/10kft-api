# Assignments

##### Endpoint: `/api/v1/users/<user_id>/assignments`
##### Endpoint: `/api/v1/projects/<project_id>/assignments`

Assignments connect a [User](users.md) to a [Project](projects.md) or a [Phase](phases.md) (part of a project) or a [LeaveType](leave-types.md).

## List assignments for a User or Project

##### Optional parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| from |  get assignments that end after this date |
| to |  get assignments that start before this date |
| per_page, page |  Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first ) |
| with_phases	| true to include assignment to phases ( child projects ) |

```
GET /api/v1/users/<user_id>/assignments

 curl 'https://vnext.10000ft.com/api/v1/users/<user_id>/assignments?auth=..'
```

```
GET /api/v1/projects/<project_id>/assignments

 curl 'https://vnext.10000ft.com/api/v1/projects/<project_id>/assignments?auth=..'
```

## Show an Assignment for a User or Project

```
GET /api/v1/users/<user_id>/assignments/<assignment_id>

 curl 'https://vnext.10000ft.com/api/v1/users/<user_id>/assignments/<assignment_id>?auth=..'
```

```
GET /api/v1/projects/project_id/assignments/<assignment_id>

 curl 'https://vnext.10000ft.com/api/v1/projects/<project_id>/assignments/<assignment_id>?auth=..'
```

Similarly, in the create and delete examples below, you can call the assignments API on projects specifying a user_id to create an assignment for that user, or to delete an assignment.

## Create an Assignment

Typical parameters: `starts_at`, `ends_at`, `allocation_mode (percent, hours_per_day, fixed)`, `percent`, `hours_per_day`, `fixed_hours`

```
POST /api/v1/users/<user_id>/assignments

 curl -d 'leave_id=<leave_id>&starts_at=<YEAR-MO-DAY>&ends_at=<YEAR-MO-DAY>'  \
                 'https://vnext.10000ft.com/api/v1/users/<user_id>/assignments?auth=...'

 curl -d 'leave_id=<leave_id>&starts_at=<YEAR-MO-DAY>&ends_at=<YEAR-MO-DAY>&percent=0.25'  \

                 'https://vnext.10000ft.com/api/v1/users/<user_id>/assignments?auth=...'

 curl -d 'leave_id=<leave_id>&starts_at=<YEAR-MO-DAY>&ends_at=<YEAR-MO-DAY>&allocation_mode=hours_per_day&hours_per_day=<hours>'  \
                 'https://vnext.10000ft.com/api/v1/users/<user_id>/assignments?auth=...'
```

## Remove an Assignment for a User

```
DELETE /api/v1/users/<user_id>/assignments/<assignment_id>

 curl -XDELETE 'https://vnext.10000ft.com/api/v1/users/<user_id>/assignments/<assignment_id>?auth=...'
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

**Notes**: `repetition_id` is used for repeated assignments. The value will be NULL when the assignment is not part or a repeating series. `repetition_id` is equal to the parent assignment.

## Repeat an Assignment

```
POST /api/v1/projects/<project_id>/assignments/<assignment_id>/repetitions
```

##### Params

| param | description |
| ------ | --------- |
| frequency_weeks | integer value of the frequency with which to repeat the assignment (e.g., 1 = every week) |
| count | integer value (less than 52) of the total number of weeks to repeat the assignment |


## Create Assignment with Subtasks

##### Endpoint: `/api/v1/assignments`

This endpoint allows an assignment to be created with subtasks. It takes all the same post parameters as a regular assignment create with the addition of the `subtasks` POST parameter. This endpoint returns the assignment object created with the nested subtasks created within it.

##### Example JSON Response

```
{
  "assignments": [
    {
        0: 
          allocation_mode: "percent"
          assignable_id: 4
          bill_rate: 1
          bill_rate_id: 4249
          created_at: "2019-08-21T15:11:08Z"
          description: ""
          ends_at: "2019-09-06"
          fixed_hours: null
          hours_per_day: null
          id: 8669
          note: ""
          organization_id: 1
          percent: 1
          repetition_id: 8668
          resource_request_id: null
          starts_at: "2019-08-30"
          status: null
          status_option_id: null
          updated_at: "2019-08-21T15:11:08Z"
          user_id: 8
      },
    "created_ids": [8771] // Deprecated
    "repetition_id": 8668
}
```

## Endpoint

```POST /api/v1/assignments```

##### Params

| param | description |
| ------ | --------- |
| subtasks | array of one or more subtask objects |

##### Example POST params

```
POST {
  "user_id": null,
  "assignable_id": 123,
  "ends_at": "2018-06-27",
  "starts_at": "2018-06-21",
  "status_option_id": 1,
  "description": "Build wireframes",
  "note": null,
  "subtasks": [
    {
      "description": "New Task",
      "completed": false
    }
  ]
}
```

##### Example JSON Response

```
{
  "data": [
    {
        "id": 12345,
        "allocation_mode": "percent",
        "percent": 1,
        "user_id": null,
        "assignable_id": 123,
        "ends_at": "2018-06-27",
        "starts_at": "2018-06-21",
        "bill_rate": null,
        "bill_rate_id": null,
        "repetition_id": null,
        "created_at": "2018-06-21T23:01:09Z",
        "updated_at": "2018-06-21T23:01:09Z",
        "all_day_assignment": true,
        "resource_request_id": null,
        "status": null,
        "status_option_id": 1,
        "description": "Build wireframes",
        "note": null,
        "subtasks": {
          "paging": {
              "self": "/api/v1/assignments/12345/subtasks?per_page=20&page=1",
              "next": null,
              "previous": null,
              "page": 1,
              "per_page": 20
          },
          "data": [
            {
              "id": 436,
              "assignment_id": 12345,
              "assignable_id": 123,
              "description": "New Task",
              "completed": false,
              "updated_at": "2018-11-01T20:00:34Z",
              "created_at": "2018-11-01T20:00:34Z",
              "updated_by": 1
            }
          ]
      }
    },
    ...
}
```

## Subtask Counts

##### Endpoint: `/api/v1/projects/<project_id>/assignments?fields=subtasks_counts`

This endpoint returns an array of subtasks counts for completed and total subtasks under each assignment record. This endpoint is a view-only endpoint.

##### Example JSON Response

```
{
  "data": [
    {
        "id": 12345,
        "allocation_mode": "percent",
        "percent": 1,
        "user_id": null,
        "assignable_id": 123,
        "ends_at": "2018-06-27",
        "starts_at": "2018-06-21",
        "bill_rate": null,
        "bill_rate_id": null,
        "repetition_id": null,
        "created_at": "2018-06-21T23:01:09Z",
        "updated_at": "2018-06-21T23:01:09Z",
        "all_day_assignment": true,
        "resource_request_id": null,
        "status": null,
        "status_option_id": 1,
        "description": "Build wireframes",
        "note": null,
        "subtask_counts": {
            "completed": 5,
            "total": 10
        }
    },
    ...
}

```

