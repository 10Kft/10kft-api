# Expense Entries

##### Endpoint: `/api/v1/users/<user_id>/expense_items`

Expense items are reported by a user on a project or leave type.

## List Expense Items for a User

##### Optional parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| from | get expenses reported on or after this date |
| to | get expenses reported on or before this date |
| per_page, page | Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first ) |

```
GET /api/v1/users/<user_id>/expense_items
curl 'https://vnext.10000ft.com/api/v1/users/1/expense_items?auth=...'
```

## Show an Expense Item For a User

```
GET /api/v1/users/<user_id>/expense_items/<expense_items_id>
curl 'https://vnext.10000ft.com/api/v1/users/1/expense_items/123
```

## Create Expense Item

When creating expense items, at least date and amount need to be specified. Project/Leave Type can be specified by one of `project_id`, `leave_type_id`, or an `assignable_id`. These three parameters refer to the same and are interchangeable. You should only specify one project/leave type parameter per expense entry call.

| `date` | `amount` | `leave_type_id` | `project_id` | `assignable_id` |

```
POST /api/v1/users/<user_id>/expense_items
curl -d 'project_id=1&date=2013-10-10&amount=100' \
    'https://vnext.10000ft.com/api/v1/users/1/expense_items'
alt. curl -d 'date=2013-10-15&expense_items=100' \
    'https://vnext.10000ft.com/api/v1/projects/987/users/1/expense_items'
```

## Update an Expense Item

```
PUT /api/v1/projects/<project_id>/users/<user_id>/expense_items/<expense_item_id>
curl -XPUT -d "amount=100"
     'href="https://vnext.10000ft.com/api/v1/projects/5/users/1/expense_items/123
```

## Delete an Expense Item

```
 DELETE /api/v1/users/<user_id>/expense_items/<expense_items_id>
curl -XDELETE
    'https://vnext.10000ft.com/api/v1/users/5/expense_items/123'
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
    "per_page": 1000,
    "page": 1,
    "previous": null,
    "self": "/api/v1/users/2/expense_items?per_page=1000&user_id=2&page=1",
    "next": null
  }
}
```
