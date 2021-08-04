# User Status

##### Endpoint: `/api/v1/users/<user_id>/statuses`

Current status for a user is a collection of Statuses.

Valid statuses are:

*   ITO (In the Office)
*   WFH (Working from home)
*   SIC (Sick)
*   OOO ( On the Road)
*   VAC (Vacation)
*   OOF (Out of office)

A new "current status" is set by simply creating a new status for the user.

## Show List of Statuses For a User

```
GET  /api/v1/users/statuses
  curl "https://api.rm.smartsheet.com/api/v1/users/7/statuses?auth=..."
```

## Create/update status for a user

##### Required Parameter:

| `status` |

##### Optional parameters:

| `assignable_id` | `current_task` | `status` | `end` | `message` |

## Usage

```
POST  /api/v1/users/<user_id>/statuses
  curl  -d 'status=OOO' \
            'https://api.rm.smartsheet.com/api/v1/users/12345/statuses?auth=...''
```

## Sample Response

```
{
    "data": [
        {
            "assignable_id": 4,
            "created_at": "2013-09-12T14:33:05Z",
            "current_task": null,
            "end": null,
            "id": 1,
            "message": "Hacking away",
            "start": null,
            "status": "ITO",
            "updated_at": "2013-09-12T14:33:05Z",
            "user_id": 1
        }
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
