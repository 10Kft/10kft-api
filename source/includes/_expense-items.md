# Expense Items

##### Endpoint: `/api/v1/users/<user_id>/expense_items`

Expense items are reported by a user on a project or leave type.

## List Expense Items for a User

##### Optional parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| from | get expenses reported on or after this date |
| to | get expenses reported on or before this date |
| per_page, page | Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first ). per_page should not exceed 1000. |


## Expenses by User

```
GET /api/v1/users/<user_id>/expense_items
GET /api/v1/users/<user_id>/expense_items/<id>
```

## Expenses by Project

```
GET /api/v1/projects/<project_id>/expense_items
GET /api/v1/projects/<project_id>/expense_items/<id>
```

## Create Expense Item

When creating expense items, at least date and amount need to be specified. Project/Leave Type can be specified by one of `project_id`, `leave_type_id`, or an `assignable_id`. These three parameters refer to the same and are interchangeable. You should only specify one project/leave type parameter per expense item call.

| `date` | `amount` | `leave_type_id` | `project_id` | `assignable_id` |

```
POST /api/v1/users/<user_id>/expense_items
```

## Update an Expense Item

```
PUT /api/v1/projects/<project_id>/users/<user_id>/expense_items/<expense_item_id>
```

## Delete an Expense Item

```
DELETE /api/v1/users/<user_id>/expense_items/<expense_items_id>
```

## Sample Response

```
{
  "data": [
    {
      "id": 1,
      "assignable_id": 32,
      "assignable_type": "Project",
      "user_id": 2,
      "amount": 10,
      "date": "2015-04-09",
      "category": null,
      "notes": "Testing exp",
      "created_at": "2015-04-09T21:54:13Z",
      "updated_at": "2015-04-09T21:54:13Z"
    }
  ]
  {
    "paging": {
    "per_page": 100,
    "page": 1,
    "previous": null,
    "self": "/api/v1/users/2/expense_items?per_page=100&user_id=2&page=1",
    "next": null
  }
}
```
