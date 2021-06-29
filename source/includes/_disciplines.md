Disciplines
=========

Disciplines currently must be created and assigned through the UI.

Endpoints:

- [Get Disciplines](#get-disciplines)
- [Get a Discipline](#get-a-discipline)


Get Disciplines
-------------

* `GET /api/v1/disciplines` will return a [paginated list](#pagination) of Disciplines.

_Optional parameters:_

- Respects [filtering parameters](#filtering)

###### Example JSON Response

```json
{
  "paging": {
    "per_page": 20,
    "page": 1,
    "previous": null,
    "self": "/api/v1/disciplines?&page=1",
    "next": null
  },
  "data": [
    {
      "id": 1,
      "value": "JavaScript Developer"
    },
    {
      "id": 2,
      "value": "Ruby Developer"
    }
  ]
}


```


Get a Discipline
-------------

* `GET /api/v1/disciplines/1` will return the role with the ID of `1`.

###### Example JSON Response

```json
{
  "id": 1,
  "value": "Developer"
}
```
