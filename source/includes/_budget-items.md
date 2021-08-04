# Project Budgets

##### Endpoint: `/api/v1/projects/<project_id>/budget_items?item_type=...`

Budget items are always specified with an "item_type" when accessed through the api. This is to keep from mixing amount and hours.

Value for `item_type` could be one of `TimeFees` / `TimeFeesDays` / `Expenses`

`TimeFeesDays` are actually in unit hours.

## List Budget Items

##### Required Parameters:

`item_type`: <value>(one of `TimeFees` / `TimeFeesDays` / `Expenses`)</value>

```
GET /api/v1/projects/<project_id>/budget_items
 curl "https://api.rm.smartsheet.com/api/v1/projects/12345/budget_items?item_type=TimeFees&auth=..
```

## Show Budget Item by id

```
curl "https://api.rm.smartsheet.com/api/v1/budget_items/6789?auth=...
 curl "https://api.rm.smartsheet.com/api/v1/projects/12345/budget_items/6789?auth=...
```

## Create a Budget Item

##### Required Parameters:

`item_type`: <value>(one of `TimeFees` / `TimeFeesDays` / `Expenses`)
`amount`: value<value></value></value>

```
curl -d "amount=5000&item_type=TimeFees"  \
            "https://api.rm.smartsheet.com/api/v1/projects/4/budget_items?auth=..."
```

## Update Budget Item by id

```
curl -XPUT -d "amount=567"  \
        "https://api.rm.smartsheet.com/api/v1/budget_items/6789?auth=..."
 or
 curl -XPUT -d "amount=567"   \
        "https://api.rm.smartsheet.com/api/v1/projects/12345/budget_items/6789?auth=..."
```

## Delete a Budget Item

```
curl -XDELETE "https://api.rm.smartsheet.com/api/v1/budget_items/6789?auth=..."
```

## Sample Response

```
{
    "data": [
        {
            "amount": 20.0,
            "assignable_id": 4,
            "assignable_parent_id": null,
            "category": "Dragging our Feet",
            "created_at": "2013-09-12T20:09:46Z",
            "id": 4,
            "item_type": "TimeFeesDays",
            "peritem_amount": null,
            "peritem_label": null,
            "updated_at": "2013-09-12T20:09:46Z"
        }
    ],
    "paging": {
        "next": null,
        "page": 1,
        "per_page": 20,
        "previous": null,
        "self": "/api/v1/projects/4/budget_items?item_type=TimeFeesDays&project_id=4&per_page=20&page=1"
    }
}
```
