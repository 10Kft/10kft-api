# Subtask Counts

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
