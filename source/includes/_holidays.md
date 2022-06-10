# Holidays

Holidays are dates that your organization treats as non-working days, and entered into Resource Management by Smartsheet by an account administrator. The API provides an endpoint for reading this information.

## Endpoints:

```
GET /api/v1/holidays
```

### Optional Query Parameters

| **Parameter** | **Description** |
| ------------- | --------------- |
| per_page, page |  Parameters for pagination. Default values are per_page = 20 , page = 1 ( the first ). per_page should not exceed 1000. |

## Fields:

| **Name** | **Type** | **Description** | **Optional** | **Readonly** |
| -------- | -------- | --------------- | ------------ | ------------- |
| `id` | number | holiday id |  | yes |
| `date` | date | the date of the holiday |  | yes |
| `name` | string | the name of the holiday |  | yes |
| `created_at` | date-time | time of creation | | yes |
| `updated_at` | date-time | time of last update | | yes |

## Examples

A holiday has the following JSON structure:

```
{
  "id": 20019,
  "date": "2015-01-01",
  "name": "New Years Day",
  "created_at": "2015-10-23T04:16:36Z",
  "updated_at": "2016-08-24T23:44:16Z"
}
```
