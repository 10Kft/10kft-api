# Projects

##### Endpoint: `/api/v1/projects`

Project is a subclass of Assignable. You will see the `id` referring to a project as `assignable_id` in other models. Sub-projects are called phases and share the same data model. A Phase has a `parent_id` that is not `null`. A project or phase can be deleted by setting the optional `archived` parameter to `true`, it can also be unarchived by setting `archived` to `false`.

Projects where `archived` is set to `true` cannot be updated. You must first unarchive (set `archived` to `false`) before updating the project.

## Project State

`project_state` describes the state of the project:

- Confirmed
- Tentative
- Internal

## List Projects (index)

##### Optional Parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| from | get projects that end on or after this date |
| to | get projects that start on or before this date |
| strict | set to `true` to restrict the projects to only those contained entirely within the `from` and `to` params |
| fields | a comma separated list, optional values [ "children", "tags", "budget_items", "project_state" , "phase_count", "summary", "custom_field_values" ] Will add additional fields to the output |
| filter_field | Specifies the property to filter on. "project_state" is the only supported value |
| filter_list | The value of "filter_field" to match, outputs will be projects with state matching this value. Possible values: Internal, Tentative, Confirmed |
| sort_field | Field to sort the return document. Possible values: created or updated |
| sort_order | order to sort the results on. Possible values: ascending or descending |
| project_code | project code to find, exact match |
| phase_name | phase name to find, exact match |
| with_archived | true to include deleted/archived projects |
| with_phases | true to include phases ( child projects ) |
| per_page, page | Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first ).  per_page should not exceed 1000. |
| archived | true to archive/false to unarchive |

## List projects

```
GET  /api/v1/projects?fields=tags,budget_items
```

## List projects with archived
```
GET  /api/v1/projects?fields=tags,budget_items&with_archived=true
```

Notes: Set `with_archived` to true to include archived projects in searches. Set `archived` to true to archive a project. Set `archived` to false to unarchive a project.

## List projects with sorting

```
GET  /api/v1/projects?sort_field=created&sort_order=ascending
```

## Filter projects

```
GET  /api/v1/projects?filter_field=project_state&filter_list=Confirmed
```

Notes: `project_state` is the only supported filter field at present.

## Show a project

```
GET  /api/v1/projects/<project_id>
```

## Show a project with its phases

```
GET  /api/v1/projects/<project_id>?fields=children
```

## Create a project
Note: You cannot add thumbnails to the project through the API

```
POST  /api/v1/projects

{
"name": "My Project",
"starts_at": "2015-03-01",
"ends_at": "2015-06-01"
}
```

## Update a Project
Note: You cannot add thumbnails to the project through the API

```
PUT  /api/v1/projects/1245

{
  "id": 1245,
  "name": "New Project Name",
  "ends_at": "2015-05-31"
}
```

## Locking Time Entries

`timeentry_lockout` is used to control when new time entries are no longer accepted to a project.

| **Value** | **Description** |
| ------------- | --------------- |
| -1 | Not locked |
| 0 | Locked |
| 7 | Locked for entries more than 7 calendar days ago. This can be any positive integer value |

Note that positive integer values in this attribute are numbers of days relative to today's date on the calendar. We do not support setting this lockout value to a specific date.

If your project has phases, note that this must also be set for each phase assignable_id for it to take effect as intended.

## Delete a Project

```
DELETE  /api/v1/projects/1245
```

## Notes:

Dates need to be in UTC

## Sample Response

```
GET  https://api.rm.smartsheet.com/api/v1/projects/<project_id>?fields=tags,summary,children,has_pending_updates&today=27-07-2016&per_page=100&auth=<token>
```

```
{
  "id":821065,
  "archived":false,
  "archived_at":null,
  "description":"",
  "guid": "xxxx-xxxx-xxxx-xxxx-xxxx-xxxx",
  "name":"Resource Management by Smartsheet Example for Wayne",
  "parent_id":null,
  "phase_name":null,
  "project_code":"",
  "secureurl":"https://10kftprojectimages.s3.amazonaws.com/a62ffd30-316f-4cb6-9c7f-eca45d07a35d/499af1a7-bc6b-446f-8535-4472e6159246.png",
  "secureurl_expiration":"3000-01-01T00:00:00Z",
  "settings":0,
  "timeentry_lockout":-1,
  "ends_at":"2015-12-31",
  "starts_at":"2015-01-01",
  "deleted_at":null,
  "created_at":"2015-11-06T18:00:40Z",
  "updated_at":"2016-04-19T18:21:16Z",
  "use_parent_bill_rates":false,
  "thumbnail":"https://10kftprojectimages.s3.amazonaws.com/a62ffd30-316f-4cb6-9c7f-eca45d07a35d/499af1a7-bc6b-446f-8535-4472e6159246.png",
  "type":"Project",
  "has_pending_updates":false,
  "client":null,
  "project_state":"Internal",
  "tags":{
    "paging":{
      "self":"/api/v1/projects/821065/tags?per_page=1&page=1",
      "next":null,
      "previous":null,
      "page":1,
      "per_page":1
    },
    "data":[
      {
        "id":1207009,
        "value":"Sales"
      }
    ]
  },
  "children":{
    "paging":{
      "self":"/api/v1/projects/821065/tags?per_page=100&page=1",
      "next":null,
      "previous":null,
      "page":1,
      "per_page":100
    },
    "data":[

    ]
  },
  "bounding_startdate":"2015-01-01",
  "bounding_enddate":"2016-07-01",
  "confirmed_hours":1283.600000000003,
  "confirmed_dollars":160450.0,
  "approved_hours":0,
  "approved_dollars":0,
  "unconfirmed_hours":87.60000000000002,
  "unconfirmed_dollars":10950.0,
  "scheduled_hours":1322.400000000003,
  "scheduled_dollars":165300.0,
  "future_hours":0,
  "future_dollars":0
}
```
