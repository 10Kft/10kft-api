# Users
##### Endpoint: `/api/v1/users`

The users collection allows you to access information about all users in the API.

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
| `user_type_id` | number | The role of the user (see below) |  | yes |
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
| `thumbnail` | string | A url to a user profile image | yes | yes |
| `created_at` | date-time | time of creation | | yes |
| `updated_at` | date-time | time of last update | | yes |

##### Optional GET parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| per_page, page | Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first )|
| fields | A comma separated list of additional fields to include in the response, optional values [ "tags", "assignments", "availabilities", "custom_field_values" ] |
| sort_field | Field to sort the return document. Possible values: `created`, `updated`, `first_name`, `last_name`, `hire_date`, `termination_date` |
| sort_order | Order to sort the results on. Possible values: `ascending` or `descending` |
| with_archived	| If set to `true`, includes archived users |
| include_placeholders	| If set to `true`, includes placeholder users |


### Deleting vs Archiving

A user cannot be deleted via the API but they may be archived by setting the optional parameter archived to true while updating a user. It can also be unarchived by setting the optional parameter archived to false. You cannot archive the account owner.

### User Type

Information about a user's role is contained in the user_type_id property.

| **user_type_id** | **Permission level** |
| ------------- | --------------- |
| 0 | None |
| 1 | Administrator |
| 2 | Project Manager |
| 3 | Team Member |
| 4 | Restricted Team Member |
| 5 | Contractor |
| 7 | Scheduler |

Values not described in this list are reserved for internal/future use.

Setting the user_type_id via API is not supported.

## Create a user
```
POST  /api/v1/users

{
  "first_name": "Chris",
  "last_name": "James",
  "email": "chris@example.com",
}
```
Creating a new user creates a resource only user. Resource only users can be used for scheduling. However, if you want the new user to be able to track their time they need to be invited through the `People` tab on your `Account Settings`.

## Sample Response
```
GET  https://api.10000ft.com/api/v1/users/1?auth=<token>
```

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
  "billability_target": 100,
  "billrate": -1,
  "has_login": true,
  "login_type": "saml",
  "thumbnail": "",
  "created_at": "2015-11-13T20:38:10Z",
  "updated_at": "2015-11-13T20:38:10Z"
}
```
