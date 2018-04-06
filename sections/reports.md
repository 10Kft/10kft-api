# Reports API

The `reports` endpoints allow you to generate report rows or totals by specifying the parameters of a report in the JSON payload of a `POST` request. The response is a JSON representation of the report rows or totals as seen in the reports UI.

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
| [`today`](#today) | string | the date on which "future scheduled" begins, in `YYYY-MM-DD` format | current UTC date |
| [`calc_incurred_using`](#calc_incurred_using) | string | one of `confirmed-unconfirmed`, `confirmed`, or `approved` | `"confirmed-unconfirmed"` |

#### Example Request Params:

```js
// POST /api/v1/reports/rows
{
  "view": "time_fees_hours",
  "time_frame": "this_week",
  "group_by": ["project_id", "user_id"],
  "filters": {
    "client": {
      "operation": "inclusion",
      "values": ["Mango Inc."]
    },
    "people_tags": {
      "operation": "exclusion",
      "values": ["intern"]
    }
  },
  "today": "2018-03-28",
  "calc_incurred_using": "confirmed-unconfirmed"
}
```

#### Example Response:

```js
{
  "params": {
    "view": "time_fees_hours",
    // ... Other request params
  },
  "dates": {
    "today": "2018-03-28",
    "range": {
      "from": "2018-03-26",
      "to": "2018-04-01"
    }
  },
  "rows": [
    {
      "project_id": 1771900,
      "project_name": "Design Planning & Management",
      "user_id": 200088,
      "user_name": "Bobby Taleb",
      "incurred_hours": 6,
      "scheduled_hours": 10,
      "difference_from_past_scheduled_hours": 0,
      "future_scheduled_hours": 4,
      "total_hours": 10
    },
    // ... More rows
  ]
}
```

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

The time frame of a report is specified as an object with "from" and "to" attributes that each specify a date in the format YYYY-MM-DD.

```js
"time_frame": {
  "from": "2018-01-01",
  "to": "2018-12-31"
}
```

There are also several shortcut strings for common time frames.

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

The `group_by` param is an array of strings that specify which attributes to group and sort rows by. Note that, while the reports UI restricts grouping to 2 levels, the API currently allows up to 5 levels.

```js
"group_by": ["client", "phase_name", "user_id", "date"]
```

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

## `today`

The `today` param is the date on which past/incurred time ends and future scheduled time begins. The expected format is "YYYY-MM-DD".

## `calc_incurred_using`

There are 3 options for calculating incurred time:

- `confirmed-unconfirmed` (default, always used in reports UI)
- `confirmed`
- `approved`

The reports UI always uses `confirmed-unconfirmed`. If your account settings specify that incurred time should use confirmed time only, the reports UI will still use the `confirmed-unconfirmed` option, but will additionally apply a default filter on `entry_type`, removing unconfirmed time, which has the same effect with regards to incurred calculations.

```json
"calc_incurred_using": "confirmed-unconfirmed",
"filters": {
  "entry_type": {
    "operation": "exclusion",
    "values": ["Unconfirmed"]
  }
}
```

The only difference between the two methods (filtering out unconfirmed time vs specifying `calc_incurred_using` as `confirmed`) is in how past scheduled time is calculated in the case where no corresponding confirmed time exists for a given day of an assignment. Filtering out unconfirmed time affects both incurred _and_ past scheduled time, whereas specifying `calc_incurred_using` as `confirmed` does not affect past scheduled time. One way to think about it is, when `calc_incurred_using` is set to `confirmed`, the report is calculated as if the "clear suggestions" button was pushed on everyone's timesheets.
