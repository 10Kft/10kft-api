# Bill Rates

Bill rates in Resource Management by Smartsheet are maintained at both the account level (defaults) and project level. When a new project is created, the account level bill rates are used as a template for setting up initial bill rates for the project. Adding a user to the project (for example, by making an assignment) causes additional user-specific rates to be created in the project. These user specific bill rates are determined by looking up the existing role and discipline specific rates and matching them up with the user's role and discipline to find the best match.

A phase is a child project and may have its own bill rate or refer to the parent project. You can add and edit phase-specific bill rates through the user interface of the application. When setting up a phase to have its own bill rate, the parent project bill rates are used as a template, much like the way account default bill rates are used as a template when setting up project bill rates. If a phase is set up to have its own bill rate, adding users to the phase results in user-specific rates being created for the phase, just like it does for projects.

The API allows you to directly manipulate project and phase specific bill rates. Changing account default bill rates are restricted to Administrators.

## Endpoints:

**Account specific bill rates**

```
GET /api/v1/bill_rates
```

**Project specific bill rates**

```
GET /api/v1/projects/<project_id>/bill_rates

GET /api/v1/projects/<project_id>/bill_rates/<id>

PUT /api/v1/projects/<project_id>/bill_rates/<id>

POST /api/v1/projects/<project_id>/bill_rates
```

### Optional Query Parameters

| **Name** | **Description** |
| ------ | --------------- |
| rebuild_assignments | rebuild ongoing and future assignments for this project with the new bill rate |

## Fields:

| **Name** | **Type** | **Description** | **Optional** | **Readonly** |
| -------- | -------- | --------------- | ------------ | ------------- |
| `id` | number | bill rate id |  | yes |
| `discipline_id` | number | discipline specific bill rate if set | yes | |
| `role_id` | number | role specific bill rate if set | yes | |
| `assignable_id` | number | the project id that the bill rate belongs to | | |
| `user_id` | number | user id for the bill rate | yes | |
| `rate` | float | bill rate | | |
| `starts_at` | date | effective start date for the bill rate | yes | |
| `ends_at` | date | effective end date for the bill rate | yes | |
| `startdate` | date | _deprecated_ | yes | |
| `enddate` | date | _deprecated_ | yes | |
| `created_at` | date-time | time of creation | | yes |
| `updated_at` | date-time | time of last update | | yes |


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
