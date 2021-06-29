# Status Options
##### Endpoint: `/api/v1/status_options`
Status options are required in order to set the `status_option_id` on [assignments](). This corresponds to the work status in the work list. Status options are account level resources and do not belong to any assignable, user, or assignment.
## Create a status option
```
POST /api/v1/status_options
```
##### Required params
| param | description |
| ----- | ----------- |
| color | one of the valid colors listed below |
| label | string |
| stage | one of the valid stages listed below |
| order | a float number used for sorting options within UI menus |

##### Valid colors
- `blue_bright`
- `blue_dark`
- `green_bright`
- `green_dark`
- `yellow`
- `orange`
- `red`
- `purple`

##### Valid stages
- `planned`
- `in_progress`
- `done`

##### Example
```
POST {
  "color": "green_bright",
  "label": "On Track",
  "stage": "in_progress",
  "order": 100.0
}
```
## List status options
```
GET /api/v1/status_options
```
Get list with deleted options.
```
GET /api/v1/status_options?with_deleted=true
```
## Show a single status option
```
GET /api/v1/status_options/<status_option_id>
```
## Update a status option
```
PUT /api/v1/status_options/<status_option_id>
```
## Delete a status option
```
DELETE /api/v1/status_options/<status_option_id>
```
In order to maintain consistency with historical data, deleting a status option only flags the resource as deleted. It does not permanently destroy the record.
