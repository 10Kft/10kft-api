# Approvals

##### Endpoint: `/api/v1/approvals`

In Resource Management by Smartsheet, certain record types are considered "approvable." Currently, these record types are time entries and expense items. Approvals are created when time entries or expense items are "submitted for approval."


## List Approvals

```
GET /api/v1/approvals
```

While you can get approvals directly from `/api/v1/approvals`, a more typical scenario is to include approvals when getting time entries or expense items by specifying "approvals" as a field. One advantage of this is that you also get "unsubmitted" records that do not yet have an associated approval record.

Example

```
GET /api/v1/users/<user_id>/time_entries

# note "fields=approvals"
curl 'https://api.rm.smartsheet.com/api/v1/users/1/time_entries?fields=approvals&auth=..'
```

Response

```json
{
  "paging": {
    ...
  },
  "data": [
    {
      "id": 123,
      "user_id": 1,
      "hours": 8,
      "scheduled_hours": null,
      ...
      "approvals": {
        "paging": {
          ...
        },
        "data": [
          {
            "id": 789,
            "status": "pending",
            "approvable_id": 123,
            "approvable_type": "TimeEntry",
            "submitted_by": 1,
            "submitted_at": "2016-10-13T01:52:09Z",
            "approved_by": null,
            "approved_at": null,
            "created_at": "2016-10-13T01:52:09Z",
            "updated_at": "2016-10-13T01:52:09Z"
          }
        ]
      }
    },
    ...
  ]
}
```

If you do get approvals from `/api/v1/approvals`, you can similarly specify "approvables" as a field.

## Submitting and Approving Approvables

```
POST /api/v1/approvals
```

Approvals are not created or updated directly. Rather, approvable records are submitted or approved through a POST request to `/api/v1/approvals`. **Note that only administrators and portfolio editors can approve time and expenses, which means that API users can only submit time and expenses, but not approve.**


##### Required parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| approvables | an array of approvable objects |
| status | either "pending" (submitting for approval) or "approved" (approving) |

##### Approvable object:

| **Parameter** | **Description** |
| ------------- | --------------- |
| id | the id of the time entry or expense item |
| type | either "TimeEntry" or "ExpenseItem" |
| updated_at | the "updated_at" time stamp of the time entry or expense item |

`updated_at` is required to ensure that the time entry or expense item has not changed since the submitter or approver has viewed it. For example, if an approver views a time entry of 4 hours and intends to approve that time, but meanwhile someone else updates the time entry to be 5 hours instead of 4, the approver might unintentionally approve a 5 hour time entry while believing they are approving a 4 hour time entry. For this reason, approvals will only be created or updated for approvables that have the correct `updated_at` value.

Example

```shell
POST /api/v1/approvals

# request body
{
  "approvables": [
    {
      "id": 123,
      "type":"TimeEntry",
      "updated_at": "2016-10-04T15:33:32Z"
    }
  ],
  "status": "pending"
}
```

Response

```
{
  "paging": {
    ...
  },
  "data": [
    {
      "id": 890,
      "status": "pending",
      "approvable_id": 123,
      "approvable_type": "TimeEntry",
      "submitted_by": 8,
      "submitted_at": "2016-10-13T20:16:40Z",
      "approved_by": null,
      "approved_at": null,
      "created_at": "2016-10-13T20:16:40Z",
      "updated_at": "2016-10-13T20:16:40Z"
    }
  ]
}
```


## Deleting Approvals

```
DELETE /api/v1/approvals/<approval_id>
```

Approvals can only be deleted if the status is "pending".
