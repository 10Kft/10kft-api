# Budget Item Categories

Budget item categories are a set of lookup values for your organization which can be used for specifying project specific budgets. These categories may represent a fee budget, a time budget, or an expense budget. The same categories may be used when reporting time or expenses to classify the budget line item the entry is to be counted against.

There is an account level definition of budget categories, made available via:

```
/api/v1/time_entry_categories
```

or

```
/api/v1/expense_item_categories 
```

in the format:

```
{
  "data": [
    {
      "category": "Time Fees Category 1",
      "id": 1083
    },
    {
      "category": "Time Fees Category 2",
      "id": 1084
    }
  ],
  "paging": {
    "next": null,
    "page": 1,
    "per_page": 20,
    "previous": null,
    "self": "/api/v1/time_entry_categories?per_page=20&page=1"
  }
}
```

## Project Specific

There is also a set of budget item categories defined at each project level, available via:

```
/api/v1/projects/<project_id>/time_entry_categories
```

or

```
/api/v1/projects/<project_id>/expense_item_categories
```

Here you get the actual budget line items defined for the project. The specific categories applicable to the project can be extracted through these.

```
{
  "id": 1132,
  "assignable_id": null,
  "assignable_parent_id": null,
  "category": 'Printing Material',
  "amount": 123,
  "item_type": "TimeFees",
  "peritem_amount": null,
  "peritem_label": null,
  "created_at": "2013-09-26T20:35:14Z",
  "updated_at": "2013-09-26T20:35:14Z"
}
```

Note that at the project level, category may also be null. This implies a project budget line item that is not assigned any particular category.

# General API Use Examples

## Fetching a Collection

```
GET /api/v1/time_entry_categories
```

or

```
GET /api/v1/expense_item_categories
```

## Sample Response

```
{
      "data": [
        {
          "category": “Design Fees",
          "id": 1083
        },
        {
          "category": “Stationary",
          "id": 1084
        }
      ],
      "paging": {
        "next": null,
        "page": 1,
        "per_page": 20,
        "previous": null,
        "self": “/api/v1/time_entry_categories?per_page=20&page=1"
      }
}
```
