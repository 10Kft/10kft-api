# Users

The users collection allows you to access information about all users in the API.

##### Optional parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| per_page, page | Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first ). per_page should not exceed 1000. |
| fields | A comma separated list of additional fields to include in the response, optional values [ "tags", "assignments", "availabilities", "custom_field_values", "approvers" ] |
| sort_field | Field to sort the return document. Possible values: `created`, `updated`, `first_name`, `last_name`, `hire_date`, `termination_date` |
| sort_order | Order to sort the results on. Possible values: `ascending` or `descending` |
| with_archived	| If set to `true`, includes archived users |
| include_placeholders	| If set to `true`, includes placeholder users |

## Endpoints

```
GET /api/v1/users

GET /api/v1/users/<id>

PUT /api/v1/users/<id>

POST /api/v1/users
```

## Fields:

| **Name** | **Type** | **Description** | **Optional** | **Readonly** |
| -------- | -------- | --------------- | ------------ | ------------- |
| `id` | number | the user id |  | yes |
| `first_name` | string | The first name |  |  |
| `last_name` | string | The last name |  |  |
| `display_name` | string | The display name |  | yes |
| `email` | string | The first name |  |  |
| `user_type_id` | number | The role of the user (see below) |  |  |
| `billable` | boolean | reserved |  |  |
| `hire_date` | date | Date user was hired | yes |  |
| `termination_date` | date | Date user was terminated | yes |  |
| `mobile_phone` | string | A phone number | yes |  |
| `office_phone` | string | A phone number | yes |  |
| `archived` | boolean | The user has been archived |  |  |
| `archived_at` | date-time | When the user was archived | yes | yes |
| `deleted` | boolean | deprecated |  |  |
| `deleted_at` | date-time | deprecated |  | yes |
| `account_owner` | boolean | Is this user the account owner | yes | yes |
| `invitation_pending` | boolean | reserved | yes | yes |
| `user_settings` | string | reserved | yes |  |
| `guid` | string | Unique id of the user |  | yes |
| `employee_number` | string | The employee number | yes |  |
| `role` | string | The role | yes |  |
| `discipline` | string | The discipline | yes |  |
| `location` | string | The location | yes |  |
| `type` | string | reserved |  | yes |
| `has_login` | boolean | The user has setup a login |  | yes |
| `login_type` | string | reserved |  | yes |
| `license_type` | string | The user's license type (see below). Defaults to `licensed` |  yes |  |
| `thumbnail` | string | A url to a user profile image | yes | yes |
| `approver_user_ids` | array of numbers | A list of other users who approve this user's timesheets | yes |  |
| `approvee_user_ids` | array of numbers | A list of other users whose timesheets this user approves | yes |  |
| `last_login_time` | date-time | Last time the user logged in | | yes |
| `created_at` | date-time | time of creation | | yes |
| `updated_at` | date-time | time of last update | | yes |

### Deleting vs Archiving

A user cannot be deleted via the API but they may be archived by setting the optional parameter archived to true while updating a user. It can also be unarchived by setting the optional parameter archived to false. You cannot archive the account owner.

### User Type

Information about a user's role is contained in the user_type_id property.

| **user_type_id** | **Permission level** |
| ------------- | --------------- |
| 0 | None |
| 1 | Resourcing Administrator |
| 2 | Portfolio Editor |
| 3 | Portfolio Reporter |
| 4 | Portfolio Viewer |
| 5 | Contractor |
| 7 | People Scheduler |
| 8 | Project Editor |

Values not described in this list are reserved for internal/future use.

API users may set the `user_type_id` of a user to any value except `1` (Administrator). Updating a user to be an administrator must be done through the app.

### License Type

Information about the user's license type is contained in the `license_type` property. Accepted values are currently `licensed` and `managed_resource`. Both types count toward the applicable limits on your plan. See Settings > People in Resource Management by Smartsheet for more information.

## Sample Response

```
{
  "id": 1,
  "first_name": "Chris",
  "last_name": "James",
  "display_name": "Chris James",
  "email": "chris@example.com",
  "user_type_id": 1,
  "billable": true,
  "hire_date": null,
  "termination_date": null,
  "mobile_phone": null,
  "office_phone": null,
  "archived": false,
  "archived_at": null,
  "deleted": false,
  "deleted_at": null,
  "account_owner": false,
  "invitation_pending": false,
  "user_settings": 1376392,
  "guid": "96d769c7-1b4e-4b07-8baf-5ed6f2b915aa",
  "employee_number": null,
  "role": "Senior",
  "discipline": "Program Management",
  "location": "Seattle",
  "type": "User",
  "license_type": "licensed",
  "billability_target": 100,
  "billrate": -1,
  "has_login": true,
  "login_type": "saml",
  "thumbnail": "",
  "approver_user_ids": [123, 456, 789],
  "approvee_user_ids": [222, 333, 444],
  "last_login_time": "2022-02-17T19:12:36Z",
  "created_at": "2015-11-13T20:38:10Z",
  "updated_at": "2015-11-13T20:38:10Z"
}
```
