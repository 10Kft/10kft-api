# Users per Project

##### Endpoint: `/api/v1/projects/<project_id>/users`

## List Users for a given Project
Users are associated to a project by [Assignments](#assignments).

##### Optional Parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| per_page, page | Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first ). per_page should not exceed 1000. |
| fields | A comma separated list of additional fields to include in the response, optional values [ "tags", "assignments", "availabilities", "custom_field_values" ] |
| sort_field | Field to sort the return document. Possible values: `created`, `updated`, `first_name`, `last_name`, `hire_date`, `termination_date` |
| sort_order | Order to sort the results on. Possible values: `ascending` or `descending` |
| with_phases |	If set to `true`, includes users who are assigned to phases ( child projects ) |
| with_archived	| If set to `true`, includes archived users |
| include_placeholders	| If set to `true`, includes placeholder users |

## List Users

```
GET  /api/v1/projects/<project_id>/users

 curl 'https://api.rm.smartsheet.com/api/v1/projects/project_id/users?fields=tags,assignments&auth=...'
```
