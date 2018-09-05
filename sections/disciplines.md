Disciplines
=========

Disciplines currently must be created and assigned through the UI.

## Endpoints

```
GET /api/v1/disciplines

GET GET /api/v1/disciplines/<id>
```

Get Disciplines
-------------

* `GET /api/v1/disciplines` will return a [paginated list](/README.md#pagination) of Disciplines.

_Optional parameters:_

- Respects [filtering parameters](/README.md#filtering)

#### Example JSON Response

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

* `GET /api/v1/disciplines/1` will return the discipline with the ID of `1`.

#### Example JSON Response

```json
{
  "id": 1,
  "value": "Developer"
}
```
