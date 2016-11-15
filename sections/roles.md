Roles
=========

Roles currently must be created and assigned through the UI.

Endpoints:

- [Get Roles](#get-roles)
- [Get a Role](#get-a-role)


Get Roles
-------------

* `GET /api/v1/roles` will return a [paginated list][pagination] of Roles.

###### Example JSON Response

```json
[
  {
    "id": 1,
    "value": "Senior"
  },
  {
    "id": 2,
    "value": "Junior"
  }
]
```

Get a Role
-------------

* `GET /api/v1/roles/1` will return the role with the ID of `1`.

###### Example JSON Response

```json
{
  "id": 1,
  "value": "Senior"
}
```
