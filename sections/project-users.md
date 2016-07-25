# Users per Project

##### Endpoint: `/api/v1/projects/<project_id>/users`

## List Users for a given Project

Users are associated to a project by [Assignments](assignments).

##### Optional Parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| fields | A comma separated list of additional fields to include in the response, optional values [ "tags", "assignments", "availabilities"] |
| per_page, page | Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first ) |

## List Users

```
GET  /api/v1/projects/<project_id>/users

 curl 'https://vnext.10000ft.com/api/v1/projects/project_id/users?fields=tags,assignments&auth=...'
```
