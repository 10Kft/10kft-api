# Availabilities

In Resource Management by Smartsheet we have the concept of a work week. It defines the days of the week that are to be considered work days and the number of work hours for those days. Given this work week, you can determine the number of work hours per day, in any given date range. The work week is configurable by an account administrator, via the account settings pages.

User availabilities are a mechanism by which you can further customize the work days for individuals in your team. When an individual has a work schedule that deviates from the normal work week observed by your team, say, because they are working part time during some time period, an administrator can specify that by adding one or more availability time blocks to that user's profile.

When a user has one or more availability time blocks specified, Resource Management by Smartsheet will always take those into consideration in addition to the normal work week information of the company.

`NB:` In the current version of the API, updating part time availabilities will NOT automatically update existing assignments and their suggested time entries to match.

### Days 0

Day0 represents Sunday of the week, day1 Monday and so on. This is irrespective of the values of start and end dates for a given availability block.

### Start and End

Availability block start and end dates specify a date range during which the given custom available hours apply. Both `starts_at` and `ends_at` values are optional. If starts_at is nil, it implies that the given availabilities are to be used infinitely into the past. Similarly a null ends_at implies that the values are to be used infinitely into the future.

Overlapping date ranges in multiple availability blocks for the same user are accepted but will produce unpredictable results.

## Endpoints:

```
GET /api/v1/users/<user_id>/availabilities

GET /api/v1/users/<user_id>/availabilities/<id>

PUT /api/v1/users/<user_id>/availabilities/<id>

DELETE /api/v1/users/<user_id>/availabilities/<id>

POST /api/v1/users/<user_id>/availabilities
```

## Fields:

| **Name** | **Type** | **Description** | **Optional** | **Readonly** |
| -------- | -------- | --------------- | ------------ | ------------- |
| `id` | number | availability block id |  | yes |
| `user_id` | number | The user id |  | yes |
| `starts_at` | date | effective start date for the availability block | yes | |
| `ends_at` | date | effective end date for the availability block | yes | |
| `day0` | number | available hours on day0 of the week | | |
| `day1` | number | available hours on day1 of the week | | |
| `day2` | number | available hours on day2 of the week | | |
| `day3` | number | available hours on day3 of the week | | |
| `day4` | number | available hours on day4 of the week | | |
| `day5` | number | available hours on day5 of the week | | |
| `day6` | number | available hours on day6 of the week | | |
| `created_at` | date-time | time of creation | | yes |
| `updated_at` | date-time | time of last update | | yes |


See more examples below.

## Examples

An availability block should have the following JSON structure:

```

{
  "id": 52,
  "user_id": 269,
  "starts_at": "2017-01-30",
  "ends_at": "2017-07-28",
  "day0": 0,
  "day1": 8,
  "day2": 8,
  "day3": 4,
  "day4": 8,
  "day5": 8,
  "day6": 0,
}
```
