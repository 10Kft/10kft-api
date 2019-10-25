# Time Entries

Time Entries are a collection of hours tracked per project and user. There are two main kinds of time_entries.

## Suggested (aka Unconfirmed) time entries

Suggested time entries (also know as unconfirmed time entries) are created by 10,000ft as a result of resources being assigned to a project. These are identifiable by the `is_suggestion: true` attribute on the time entry objects. Suggested time entries are not returned by the API by default and must be requested using the `with_suggestions=true` parameter on the GET API call to fetch time entries.

Suggested time entries are read-only and are kept up to date by 10Kft as the corresponding assignments are updated.

## Confirmed time entries.

Confirmed time entries are what a user (or the API) has explicitly created to indicate that they have spent some time working on a project.

## Time Entries and Resource Only Users

Note that just like in the application UI, you cannot create new confirmed time entries for resource only users via the API. You can read suggested time entries for all users via the API.

## Bill Rates

Time entries have an associated bill rate attached to them. When a new time entry is created, 10Kft will determine the appropriate bill rate for it (based on your account and project settings) and assign a values. When reading time entries, you can see this assigned bill rate.

## Fields

| **Name** | **Type** | **Description** | **Optional** | **Readonly** |
| -------- | -------- | --------------- | ------------ | ------------- |
| `id` | number | Time entry id |  | yes |
| `user_id` | number | User or resource id |  |  |
| `assignable_id` | number | Project or leave type id |  |  |
| `assignable_type` | string | Project or LeaveType |  |  |
| `date` | date | The date |  |  |
| `hours` | number | Number of hours confirmed |  |  |
| `is_suggestion` | boolean | Is this a suggested time entry |  | yes |
| `scheduled_hours` | number | Number of hours scheduled (if this is a suggested time entry) |  |  |
| `task` | string | A task category | yes |  |
| `notes` | string | A note | yes |  |
| `bill_rate` | number | The hourly rate for the time entered |  |  |
| `bill_rate_id` | number | The rate id reference |  |  |
| `created_at` | date-time | time of creation | | yes |
| `updated_at` | date-time | time of last update | | yes |

## Endpoints:

```
# Time entries by user
GET /api/v1/users/<user_id>/time_entries
GET /api/v1/users/<user_id>/time_entries/<id>

# Time entries for given date-range
GET /api/v1/users/<user_id>/time_entries?from=2017-03-14&to=2017-03-21  

# Time entries by project
GET /api/v1/projects/<project_id>/time_entries
GET /api/v1/projects/<project_id>/time_entries/<id>

# All time entries in the account
GET /api/v1/time_entries
GET /api/v1/time_entries/<id>

# Time entries for given date-range
GET /api/v1/time_entries?from=2017-03-14&to=2017-03-21  

# Updating a time entry
PUT /api/v1/users/<user_id>/time_entries/id

# Deleting a time entry
DELETE /api/v1/users/<user_id>/time_entries/id

```

### Optional Query Parameters:

| **Name** | **Description** | format |
| ------------- | --------------- | --------------- |
| from | get projects that start on or after this date | &from=2017-03-14 |
| to | get projects that end on or before this date | &to=2017-03-21 |
| sort_field | Field to sort the return document. Possible values: created or updated |
| sort_order | order to sort the results on. Possible values: ascending or descending |
| with_suggestions | true to include suggested (unconfirmed) time entries based on assignments on the schedule | &with_suggestions=true |

> IMPORTANT: *to* and *from* _must_ be a valid date formatted as `yyyy-mm-dd`

### Creating Time Entries

When creating time entries, a valid user_id, assignable_id, date and hours must be supplied. Assignable id can be `assignable_id`, `project_id` or `leave_type_id`.

You can optionally specify values for `task` and `notes`, which must be fewer than 256 characters in length. If you know a valid `bill_rate_id` matching the user and project of the time entry, you can specify that at the time of creating a time entry as well.

```
POST /api/v1/users/<user_id>/time_entries

{
  "user_id": <user_id>,
  "assignable_id": 1001,
  "date": "2012-01-21",
  "hours": 0.5,
  "task": 'Travel',
  "notes": 'Drive to Seattle, WA to meet with 10Kft'
}
```

Note that the user_id in the URL must match the user_id in the POST data in the above example. In this example, the user_id in post data is optional. Similar rules apply when you manipulate time entries within a project time entries collection, like below

```
POST /api/v1/projects/<project_id>/time_entries

{
  "user_id": 123,
  "assignable_id": <project_id>,
  "date": "2012-01-01",
  "hours": 4.0,
}
```

## Examples

A confirmed time entry (note `is_suggestion` is false).

```
{
  "id":100001,
  "user_id": 123,
  "assignable_id": 1001,
  "assignable_type": "Project",
  "date": "2013-09-11",
  "hours": 8.0,
  "is_suggestion": false,
  "scheduled_hours": null,
  "task": null,
  "bill_rate": 150,
  "bill_rate_id": 4,
  "created_at": "2013-09-12T04:32:28Z",
  "updated_at": "2013-09-18T04:32:28Z"
}
```

A suggested time entry (note is_suggestion is true) and hours are given in `scheduled_hours` instead of `hours`. Task and notes are null in suggested time entries as well.

```
{
  "id":100000,
  "user_id": 123,
  "assignable_id": 1001,
  "assignable_type": "Project",
  "date": "2013-09-11",
  "hours": null,
  "is_suggestion": true,
  "scheduled_hours": 8.0,
  "task": null,
  "notes": null,
  "bill_rate": 150,
  "bill_rate_id": 4,
  "created_at": "2013-09-12T04:32:28Z",
  "updated_at": "2013-09-18T04:32:28Z"
}
```
