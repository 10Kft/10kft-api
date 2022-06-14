# Placeholder Resources

##### Endpoint: `/api/v1/placeholder_resources`

Placeholder resources can be used for temporary resourcing on projects where the final resources are not yet known. Placeholders behave quite similarly to users, with a few differences discussed below.

## List Placeholder Resources (index)

##### Optional Parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| fields | A comma separated list of additional fields to include in the response [ "assignments", "custom_field_values"] |
| per_page, page | Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first ). per_page should not exceed 1000. |

```
GET  /api/v1/placeholder_resources
 curl 'https://api.rm.smartsheet.com/api/v1/placeholder_resources?fields=assignments,custom_field_values&auth=...'
```

Note that custom field values can only be accessed if custom fields are enabled for the account. This is only possible for pro plans and up. See [custom fields](#custom-fields) for details.

## Show Placeholder

##### Optional Parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| fields | A comma separated list of additional fields to include in the response [ "assignments", "custom_field_values"] |
| per_page, page | Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first ). per_page should not exceed 1000. |

```
GET  /api/v1/placeholder_resources/<placeholder_resource_id>
 curl 'https://api.rm.smartsheet.com/api/v1/placeholder_resources/12345?fields=assignments&auth=...'
```

## Create a Placeholder Resource

##### Required Parameters

* title

```
POST  /api/v1/placeholder_resources
 curl -d 'title=Designer' \
             'https://api.rm.smartsheet.com/api/v1/placeholder_resources?auth=...'
```

Placeholders are referred to by title. The title is displayed wherever placeholders appear in the application e.g., on projects, the schedule, etc. Therefore, it is required to specify this parameter.

##### Optional Parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| role | The placeholder's [role](#roles) in the organization. |
| discipline | The placeholder's [discipline](#disciplines). |
| location | The organizational location the placeholder belongs to. |

##### Parameters not exposed through the API

In the application's user interface, there are certain options available when creating and editing placeholder resources. For example, if a role and discipline are selected, the placeholder title is auto-populated as a combination of discipline and role. For example, a placeholder with discipline 'Engineering' and role 'Director' would be auto-assigned the title 'Engineering, Director'. Options also exist to upload a thumbnail image for the placeholder, or to choose a color and abbreviation and then auto-generate a thumbnail. These options are currently not available through the API, and can only be used via the user interface.

## Update a Placeholder

Placeholder specified by `id`

```
PUT  /api/v1/placeholder_resources/<placeholder_resource_id>
 curl -XPUT -d 'title=Senior Designer' \
             'https://api.rm.smartsheet.com/api/v1/placeholder_resources/12345?auth=...'
```

## Delete a Placeholder

Placeholder resources may be deleted via the API, as follows.

```
DELETE  /api/v1/placeholder_resources/<placeholder_resource_id>
 curl -XDELETE \
             'https://api.rm.smartsheet.com/api/v1/placeholder_resources/12345?auth=...'
```

## Placeholders and Users/People

As noted above, placeholders behave similarly to real users in certain cases. However, there are some key differences. Here we discuss ways in which placeholders can be used similar to users in the API, and ways they are different.

##### Placeholder Assignments

Assignments can be made, updated, and removed via the [Assignments](#assignments) API just as they can for users.
The only difference is that this is accessed through the `placeholder_resources` endpoint. In general, for the [Assignments](#assignments) API, a placeholder resource ID can be used as the `user_id` parameter.

```
GET  /api/v1/placeholder_resources/<placeholder_resource_id>/assignments
 curl 'https://api.rm.smartsheet.com/api/v1/placeholder_resources/12345/assignments?&auth=...'
```

##### Placeholder Bill Rates

If a placeholder is given a role/discipline, they will inherit account default bill rates for that role/discipline. Specific bill rates can also be created for placeholders using the [bill rates](#bill-rates) API. A placeholder ID can be specified as the user_id parameter. No additional parameters are required.

##### Placeholder Custom Fields

[Custom fields](#custom-fields) can be created for placeholders through the application UI. API docs coming soon.

##### Placeholder Time Entries
Time tracking for placeholders is not supported - i.e. it is not possible to create or edit time entries for a placeholder. However, system-generated suggested entries are supported for placeholders. When a placeholder is assigned to a project, the system will generate scheduled hours based on the type of assignment and update budget projections, so that placeholders can be used for forecasting/projection. However, placeholders do not incur time, and no explicit time entry changes can be made for them. System-generated time entries for placeholders can be viewed via the [time entries](#time-entries) API, by passing in the placeholder ID as the user_id parameter, similar to assignments.

##### Not Supported: Expense Items and Tags

Expense items are not available for placeholders.

Tags for placeholders are also not supported. [Custom fields](#custom-fields) should be used instead.

## Placeholders on a Project

Similar to [users on a project](#users-per-project), you can get the placeholder resources assigned to a project using the following API endpoint:

```
/api/v1/projects/<project_id>/placeholder_resources
```
