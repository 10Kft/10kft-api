# Reports API

The `reports` endpoints allow you to generate report rows or totals by specifying the parameters of a report in a `POST` request. The response is a JSON representation of the report rows or totals as seen in the reports UI.

## Endpoints

- `/api/v1/reports/rows`
- `/api/v1/reports/totals`

## Parameters

With the exception of `today` and `calc_incurred_using`, each of the following parameters has a corresponding menu in the reports UI.

| param | data type | description | default |
| ----- | --------- | ----------- | ------- |
| [`view`](#view) | string | the name of the view (e.g. `time_fees_hours`, `utilization`, etc.) | `"time_fees_hours"` |
| [`time_frame`](#time_frame) | object or string | a custom time frame object or the name of the time frame | `"this_week"` |
| [`group_by`](#group_by) | array of strings | the attributes to group rows by | `["project_id"]` (or `["user_id"]` for utilization) |
| [`filters`](#filters) | object of objects | the attributes and values to include or exclude | `null` |
| `today` | string | the date on which "future scheduled" begins, in `YYYY-MM-DD` format | current UTC date |
| `calc_incurred_using` | string | one of `confirmed-unconfirmed`, `confirmed`, or `approved` | `"confirmed-unconfirmed"` |


## `view`

There are currently ten supported views, which correspond to the reports available in the reports UI. The view determines which columns are returned.

#### Time and Fees

- `time_fees_hours`
- `time_fees_days`
- `time_fees_amounts`
- `time_fees_hours_and_amounts`
- `time_fees_days_and_amounts`

#### Budgets

- `budgets_hours`
- `budgets_days`
- `budgets_amounts`

#### Utilization, Expenses

- `utilization`
- `expenses`

## `time_frame`

The time frame of a report is specified as an object with "from" and "to" attributes that each specify a date in the format YYYY-MM-DD. There are also several shortcut strings for common time frames.

- `this_week`
- `this_month`
- `this_quarter`
- `this_year`
- `last_week`
- `last_month`
- `last_quarter`
- `last_year`
- `next_30`
- `next_60`
- `next_90`
- `last_30`
- `last_60`
- `last_90`
- `last_and_next_90`

## `group_by`

The following are all the valid attributes that rows can be grouped by. Note that utilization reports have an additional restriction such that rows can only be grouped by user attributes or date attributes.

#### User Attributes

- `user_id`
- `role`
- `discipline`
- `location`
- `assignment_status`

#### Date Attributes

- `date`
- `week`
- `month`

#### Assignable Attributes

- `project_id`
- `client`
- `leave_type`
- `project_type`
- `project_state`
- `phase_name`

#### Time Entry or Expense Attributes

- `record_type`
- `entry_type`
- `category`
- `approval_status`
- `approved_by`

## `filters`

Attributes that can be used as grouping values can also be used as filters. Additionally, the following attributes can be used as filters as well.

- `people_tags`
- `project_tags`
- `custom_fields`

The `filters` parameter is expected to be an object where the keys are the attribute names, and the values are objects that specify what to filter on. The filter objects are expected to specify an `operation` and an array of `values`. `operation` can be either `inclusion` or `exclusion`. The `values` array may contain either integers or strings, depending on the attribute.

```json
"filters": {
  "project_id": {
    "operation": "inclusion",
    "values": [432, 561, 642]
  },
  "people_tags": {
    "operation": "exclusion",
    "values": ["intern"]
  }
}
```

Filtering on `custom_fields` is slightly different in that, instead of a single object with an `operation` and `values`, the expectation is an array of objects, each with an `operation`, `values`, and `id`, which is the custom field id.

```json
"filters": {
  "custom_fields": [
    {
      "id": 4321,
      "operation": "inclusion",
      "values": ["E", "S", "R"]
    },
    {
      "id": 5678,
      "operation": "exclusion",
      "values": ["tentative"]
    }
  ]
}
```
