# Leave Types

##### Endpoint: `/api/v1/leave_types`

LeaveType is a subclass of Assignable. You will see the id refering to a project as `assignable_id` in other models. LeaveType is an assignable that you can assign time to, not being part of a project, such as Vacation.

## List Leave Types (index)

```
GET  /api/v1/leave_types

 curl 'https://api.rm.smartsheet.com/api/v1/leave_types?auth=...'
```

## Show a LeaveType

```
GET  /api/v1/leave_types/<leave_type_id>

 curl 'https://api.rm.smartsheet.com/api/v1/leave_types/12345?auth=...'
```

## Sample Response

```
{
    "data": [
        {
            "id": 2,
            "name": "Sick",
            "description": null,
            "guid": "FAFC777B-8CD2-4434-9C0E-59366A1A65B9",
            "deleted_at": null,
            "created_at": "2013-09-10T21:31:06Z",
            "updated_at": "2013-09-10T21:31:06Z"
        }
    ],
    "paging": {
        "next": null,
        "page": 1,
        "per_page": 20,
        "previous": null,
        "self": "/api/v1/leave_types?per_page=20&page=1"
    }
}
```
