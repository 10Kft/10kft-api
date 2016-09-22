# Bill Rates by Project

##### Endpoint: `/api/v1/projects/<project_id>/bill_rates`

##### Fields:

| **ID** | **Description** |
| ------ | --------------- |
| id | bill rate id |
| rate | bill rate |
| assignable_id | the project id that the bill rate belongs to |
| discipline_id | discipline specific bill rate if set |
| role_id | role specific bill rate if set |
| user_id | user id for the bill rate |
| id | Bill rate id |
| startdate | effective start date for the bill rate |
| enddate | effective end date for the bill rate |

## Query String Arguments

`rebuild_assignments`: rebuild all assignments for this project with the new bill rate

## List Bill Rates For Project

```
curl \
'https://vnext.10000ft.com/api/v1/projects/1/bill_rates?auth=...'
```

## List Individual Bill Rate

```
curl \
'https://vnext.10000ft.com/api/v1/projects/1/bill_rates/123?auth=...'
```

## Update Individual Bill Rate

```
PUT /api/v1/projects/<project_id>/bill_rates/<bill_rate_id>
curl -XPUT -d 'bill_rate=500' \
'https://vnext.10000ft.com/api/v1/projects/1/bill_rates/123'
```

## Create New Bill Rate

##### Required Parameters

| `user_id` | `bill_rate` | `assignable_id` |

```
curl -d 'user_id=12345,bill_rate=250,assignable_id=67890' 'https://vnext.10000ft.com/api/v1/projects/1/'
```

## Sample Response

```
{
    {
    "data":[
      {
        "id":991618,
        "rate":225.0,
        "assignable_id":109313,
        "discipline_id":null,
        "role_id":30,
        "user_id":null,
        "startdate":"2013-09-27T00:00:00Z",
        "enddate":null,
        "created_at":"2013-09-27T22:10:24Z",
        "updated_at":"2013-09-27T22:10:24Z"},
      {
        "id":991619,
        "rate":225.0,
        "assignable_id":109313,
        "discipline_id":null,
        "role_id":30,
        "user_id":null,
        "startdate":"2013-09-27T00:00:00Z",
        "enddate":null,
        "created_at":"2013-09-27T22:10:24Z",
        "updated_at":"2013-09-27T22:10:24Z"}
      ]
      "paging":{
        "per_page":20,
        "page":1,
        "previous":null,
        "self":"/api/v1/projects/109313/bill_rates?project_id=109313&page=1",
        "next":"/api/v1/projects/109313/bill_rates?project_id=109313&page=2"
      }
    }


```
