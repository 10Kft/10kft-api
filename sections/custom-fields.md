# Custom Fields and Custom Field Values

## Custom Fields

##### Endpoint `/api/v1/custom_fields`

## Fields:

| **Name** | **Type** | **Description** | **Optional** | **Readonly** |
| -------- | -------- | --------------- | ------------ | ------------- |
| `id` | number | custom field id | n/a | readonly |
| `namespace` | string | either `assignables` or `users` | required | readonly |
| `data_type` | string | can be `string`, `selection_list`, or `multiple_choice_selection_list`| required | readonly |
| `name` | string | name of the custom field | required | editable |
| `description` | string | description of the custom field | optional | editable |
| `default_value` | string | the value to be applied if none is specified | optional | editable |
| `is_visible_on_info_page` | boolean | boolean value, defaults to `true` | optional | editable |
| `is_visible_as_filter` | boolean | boolean value, defaults to `false` | optional | editable |
| `options` | array | array of possible values (only applies to `selection_list` and `multiple_choice_selection_list`) | required (only for selection lists) | editable |

### Creating Custom Fields
```
POST /api/v1/custom_fields
```
##### Required parameters:

| **Parameter** | **Type** | **Description** |
| ------------- | -------- | --------------- |
| `namespace` | string | either `assignables` or `users` |
| `name` | string | the name of the field |
| `data_type` | string | can be `string`, `selection_list`, or `multiple_choice_selection_list`|
| `options` | array | array of possible values (only applies to `selection_list` and `multiple_choice_selection_list`) |

##### Optional parameters:

| **Parameter** | **Type** | **Description** |
| ------------- | -------- | --------------- |
| `description` | string | a short description of the field |
| `default_value` | string | the value to be applied if none is specified |
| `is_visible_on_info_page` | boolean | boolean value, defaults to `true` |
| `is_visible_as_filter` | boolean | boolean value, defaults to `false` |
| `apply_default_to_existing_objects` | boolean | non-persisting boolean value that, if `true`, triggers a one time application of the default value to all existing projects or users |

Example:
```
POST /api/v1/custom_fields
{
  "name": "Skills",
  "namespace": "users",
  "is_visible_on_info_page": true,
  "is_visible_as_filter": true,
  "data_type": "multiple_choice_selection_list",
  "options": [
    "Audio/Video",
    "Graphic Design",
    "UX",
    "Analytics",
    "Python",
    "Ruby",
    "JavaScript"
  ]
}
```

### Updating Custom Fields
```
PUT /api/v1/custom_fields/<custom_field_id>
```
##### Editable parameters:

| **Parameter** | **Type** | **Description** |
| ------------- | -------- | --------------- |
| `name` | string | the name of the field |
| `description` | string | a short description of the field |
| `options` | array | array of possible values (only applies to `selection_list` and `multiple_choice_selection_list`) |
| `default_value` | string | the value to be applied if none is specified |
| `is_visible_on_info_page` | boolean | boolean value, defaults to `true` |
| `is_visible_as_filter` | boolean | boolean value, defaults to `false` |

> :warning: When removing a value from `options` that is also the `default_value`, the `default_value` needs to be updated as well.

### Getting Custom Fields
```
GET /api/v1/custom_fields
GET /api/v1/custom_fields/<custom_field_id>
```

### Deleting Custom Fields
```
DELETE /api/v1/custom_fields/<custom_field_id>
```

Deleting a custom field will also delete all of its associated custom field values.

## Custom Field Values

##### Endpoints
```
/api/v1/projects/<project_id>/custom_field_values
/api/v1/users/<user_id>/custom_field_values
```

## Fields:

| **Name** | **Type** | **Description** | **Optional** | **Readonly** |
| -------- | -------- | --------------- | ------------ | ------------- |
| `id` | number | custom field value id | n/a | readonly |
| `custom_field_id` | number | `id` of the associated custom field | required | readonly |
| `user_id` or `project_id` | number | `id` of the associated user or assignable | required | readonly |
| `value` | string or array | the actual value | required | editable |

### Creating Custom Field Values
```
POST /api/v1/projects/<project_id>/custom_field_values
POST /api/v1/users/<user_id>/custom_field_values
```
##### Required parameters:

| **Parameter** | **Type** | **Description** |
| ------------- | -------- | --------------- |
| `custom_field_id` | number | `id` of the associated custom field |
| `user_id` or `project_id` | number | `id` of the associated user or assignable (can be inferred from URL) |
| `value` | string or array | the actual value |

**Note**: Only custom fields with a `data_type` of `multiple_choice_selection_list` can accept an array with multiple values as its `value` in a `POST` request. Note that this array is treated as the complete set of values for the given custom field and project/user. Subsequent `POST` requests for the same custom field and project/user will result in the deletion of previous values if those values are not also included in the `value` array. In other words, subsequent `POST` requests do not _append_ new values, but rather _replace_ the _set_ of values as a whole.

### Updating Custom Field Values
```
PUT /api/v1/projects/<project_id>/custom_field_values/<id>
PUT /api/v1/users/<user_id>/custom_field_values/<id>
```
##### Editable parameters:

| **Parameter** | **Type** | **Description** |
| ------------- | -------- | --------------- |
| `value` | string | the actual value |

### Getting Custom Field Values
```
GET /api/v1/projects/<project_id>/custom_field_values
GET /api/v1/users/<user_id>/custom_field_values
```
In addition to getting custom field values directly, you can also include custom field values as a nested collection when getting users or projects by specifying `custom_field_values` in the `fields` parameter.
```
GET /api/v1/projects/<project_id>?fields=custom_field_values
GET /api/v1/users/<user_id>?fields=custom_field_values
```

### Deleting Custom Field Values

Custom field values cannot be deleted directly. To delete all custom field values that belong to a specific custom field, you can delete that custom field itself, and all associated values will be deleted as well.
