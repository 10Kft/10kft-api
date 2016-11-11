Roles
=========

_Description TBD_

Endpoints:

- [Get Roles](#get-roles)
- [Get a Role](#get-a-role)
- [Create a Role](#create-a-role)
- [Update a Role](#update-a-role)
- [Destroy a Role](#destroy-a-role)

Get Roles
-------------

* `GET /api/v1/roles` will return a [paginated list][pagination] of Roles visible to the current user.


Get a Role
-------------

* `GET /api/v1/roles/1` will return the Role with the given ID, granted they have permission.


Create a Role
-------------

* `POST /api/v1/roles` will return the Role with the given ID, granted they have permission.


Update a Role
-------------

* `PUT /api/v1/roles` will return the Role with the given ID, granted they have permission.


Destroy a Role
-------------

* `DELETE /api/v1/roles` will return the Role with the given ID, granted they have permission.
