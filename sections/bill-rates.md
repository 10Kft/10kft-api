# Bill Rates

Bill rates in 10Kft are maintained at both the account level (defaults) and project level. When a new project is set up, the account-level bill rates are used as a template for setting up initial bill rates for the project. Once account defaults are copied to a project, adding a user to the project (for example, by making an assignment).

Phases which are a child project may also have their own bill rates or refer to the parent project. Phase bill rates are set up for a project by specifying that the phase should have its own bill rates. This is accomplished through the user interface in the application. While editing the project in Plans, you can add or edit phase-specific bill rates. Much like how account defaults are used as a template when setting up project bill rates, the parent project bill rates are used as a template when setting up a phase to have its own bill rates.

When an assignment is made or a time entry is added to a project, we check to see if the `user_id` of that assignment or time entry already has a project specific bill rate. If one is not found, we will use that user's role and discipline to look up a matching rate, based on data found in the project bill rates, and create a new user specific bill rate with that value. From this point on, you can edit this user specific rate to customize it as needed.

The API allows you to directly manipulate project and phase specific bill rates. Changing account default bill rates are restricted to Administrators.

## Endpoints:

**Account specific bill rates**

```
GET /api/v1/projects/bill_rates
```

**Project specific bill rates**

```

GET /api/v1/projects/<project_id>/bill_rates

GET /api/v1/projects/<project_id>/bill_rates/<id>

PUT /api/v1/projects/<project_id>/bill_rates/<id>

DELETE /api/v1/projects/<project_id>/bill_rates/<id>

POST /api/v1/projects/<project_id>/bill_rates
```

### Optional Query Parameters

| **Name** | **Description** |
| ------ | --------------- |
| rebuild_assignments | rebuild all assignments for this project with the new bill rate |

## Fields:

| **Name** | **Type** | **Description** | **optional** |
| -------- | -------- | --------------- | ------------ |
| `id` | number | bill rate id |  |
| `discipline_id` | number | discipline specific bill rate if set | yes |
| `role_id` | number | role specific bill rate if set | yes |
| `assignable_id` | number | the project id that the bill rate belongs to |  |
| `user_id` | number | user id for the bill rate | yes |
| `rate` | float | bill rate |  |
| `starts_at` | date | effective start date for the bill rate | yes |
| `ends_at` | date | effective end date for the bill rate | yes |
| `startdate` | date | _deprecated_ | yes |
| `enddate` | date | _deprecated_ | yes |

Project-specific bill rates editable via the API require a valid `assignable_id` attribute value.

Project and user specific bill rate must not specify a `role_id` or `discipline_id`, because a specific user has been chosen and role and discipline do not apply for such a bill rate.

See more examples below.

## Examples

A bill rate should have the following JSON structure:

```
/* project default rate */

{
  "id":991618,
  "rate":100.0,
  "discipline_id":null,
  "role_id":30,
  "assignable_id":1234,
  "user_id":null,
  "starts_at":null,
  "ends_at":null,
  "created_at":"2013-09-27T22:10:24Z",
  "updated_at":"2013-09-27T22:10:24Z"
}

/* project rate for discipline id 15 */

{
  "id":991618,
  "rate":100.0,
  "discipline_id":15,
  "role_id":30,
  "assignable_id":1234,
  "user_id":null,
  "starts_at":null,
  "ends_at":null,
  "created_at":"2013-09-27T22:10:24Z",
  "updated_at":"2013-09-27T22:10:24Z"
}
```

Account-specific bill rates will not have an `assignable_id` or a `user_id`, and will look like below. They may optionally have a `role_id` or `discipline_id`, to indicate a default rate for that role and/or discipline.

```
{
  "id":991618,
  "rate":200.0,
  "discipline_id":null,
  "role_id":null,
  "assignable_id":null,
  "user_id":null,
  "starts_at":null,
  "ends_at":null,
  "created_at":"2013-09-27T22:10:24Z",
  "updated_at":"2013-09-27T22:10:24Z"
}
```

User-specific bill rates on a project will have an `assignable_id` and a `user_id`. They may optionally also have a `starts_at` and `ends_at` values to indicate that the particular rate is applicable to a specific date range. When date range-specific bill rates are added via the API, they will be preferred over the default rate for the same user. This preference is determined based on the start date of the assignment or time entry in question.

```
{
  "id":991618,
  "rate":100.0,
  "discipline_id":null,
  "role_id":null,
  "assignable_id":123,
  "user_id":1001,
  "starts_at":"2013-09-27T00:00:00Z",
  "ends_at":null,
  "created_at":"2013-09-27T22:10:24Z",
  "updated_at":"2013-09-27T22:10:24Z"
}
```
