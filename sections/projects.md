# Projects

##### Endpoint: `/api/v1/projects`

Project is a subclass of Assignable. You will see the `id` referring to a project as `assignable_id` in other models. Sub-projects are called phases and share the same data model. A Phase has a `parent_id` that is not `null`. A project or phase can be deleted by setting the optional `archived` parameter to `true`, it can also be unarchived by setting `archived` to `false`.

Projects where `archived` is set to `true` cannot be updated. You must first unarchive (set `archived` to `false`) before updating the project.

## Project State

`project_state` describes the state of the project:

| Confirmed | Tentative | Internal |

## Locking Time Entries

`timeentry_lockout` is marked as -1 when the the feature is disabled. When `timeentry_lockout` >= 0 indicates how old time entries can be before they are locked and cannot be changed.

## List Projects (index)

##### Optional Parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| from | get projects that start on or after this date |
| to | get projects that end on or before this date |
| fields | a comma separated list, optional values [ "tags", "budget_items", "project_state" , "phase_count", "summary" ] Will add additional fields to the output |
| filter_field | Specifies the property to filter on. "project_state" is the only supported value |
| filter_list | The value of "filter_field" to match, outputs will be projects with state matching this value. Possible values: Internal, Tentative, Confirmed |
| sort_field | Field to sort the return document. Possible values: created or updated |
| sort_order | order to sort the results on. Possible values: ascending or descending |
| project_code | project code to find, exact match |
| phase_name | phase name to find, exact match |
| with_archived | true to include deleted/archived projects |
| with_phases | true to include phases ( child projects ) |
| per_page, page | Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first )|
| archived | true to archive/false to unarchive |

## List projects

```
GET  /api/v1/projects?fields=tags,budget_items
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

## List projects with sorting

```
GET  /api/v1/projects?sort_field=created&sort_order=ascending
```

## Create a project

```
POST  /api/v1/projects

{
"name": "My Project",
"starts_at": "2015-03-01",
"ends_at": "2015-06-01"
}
```

## Update a Project

```
PUT  /api/v1/projects/1245

{
  "id": 1245,
  "name": "New Project Name",
  "ends_at": "2015-05-31"
}
```

## Delete a Project

```
DELETE  /api/v1/projects/1245
```

## Notes:

Dates need to be in UTC

## Sample Response

```
{
  "archived": false,
  "client": "ABCDE",
  "created_at": "2013-09-12T04:32:28Z",
  "deleted_at": null, # deprecated look at "archived_at"
  "archived_at": null,
  "description": null,
  "ends_at": "2013-09-18",
  "guid": "52b13423-9185-4ed6-9992-ae9ebe8ff204",
  "has_pending_updates": true, # only appears in show, not index calls
  "id": 4,
  "name": "Klaras Birthday",
  "parent_id": null,
  "phase_name": null,
  "project_code": "",
  "project_state": "Confirmed",
  "secureurl": null,
  "secureurl_expiration": null,
  "settings": 0,
  "starts_at": "2013-09-11",
  "thumbnail": null,
  "timeentry_lockout": -1,
  "updated_at": "2013-09-12T04:32:28Z"
}
```
