# Project Membership

##### Endpoint: `/api/v1/users/:id/project_memberships`
##### Endpoint: `/api/v1/projects/:id/project_members`

The first endpoint will return a set of `project_id`s given a `user_id`. The second endpoint will return a set of `user_id`s given a single `project_id`.

## Project Memberships

## List

```
GET /api/v1/users/:id/project_memberships?membership=level
```

```
GET|POST /api/v1/relationships/project_memberships?user_ids=id,id,id&membership=level
```

Both will get a list of `Project`s which the user or users are a member of, at the provided level.
In the case where no membership level is given, the GET defaults to `member` ie. any level. Valid membership levels include: member, viewer, reporter, scheduler, and editor.

Result: Paginated API result, `data` field will consist of tuples that look similar to the following:
`{"id": 1234, uid: "Project-1234", name: "Project Name"}`

## Set

```
POST /api/v1/users/:id/project_memberships
```

This API call replaces the user's project memberships. JSON body should include a `relationships` field with `[project_id, membership_level]` tuples.

NOTE: This replaces the membership list. If you leave off a project, the user will be REMOVED from that project. If the user was already a member of a project, their membership will be changed to the level specified. If the user was not previously a member of a project, they will be added with the level specified.

```
PUT /api/v1/users/:id/project_memberships
```

This API call updates the user's project memberships. JSON body should include a `relationships` field with `[project_id, membership_level]` tuples.

NOTE: This updates the membership list. If you leave off a project, the user’s relationship to that project will be unchanged. If the user was already a member of a project, their membership will be changed to the level specified. If the user was not previously a member of a project, they will be added with the level specified.

## Remove
```
DELETE /api/v1/users/:id/project_memberships
```
This API call removes the single user from the project's membership list. JSON body should include a `project_ids` field, which is an array of `[project_id, project_id, ...]`.

## Project Members
This section contains endpoints pertaining to the members of a particular project.

## List

```
GET /api/v1/projects/:id/project_members?membership=level
```

```
GET|POST /api/v1/relationships/project_members?project_ids=id,id,id&membership=level
```

Both will get a list of `User`s who are members of the project or projects, at the provided level.
In the case where no membership level is given, the GET defaults to `member` ie. any level. Valid membership levels include: member, viewer, reporter, scheduler, and editor.

Result: Paginated API result, `data` field will consist of tuples that look similar to the following:
`{"id": 1234, uid: "User-1234", name: "User's Name"}`

## Set

```
POST /api/v1/projects/:id/project_members
```

This API call replaces the project's membership list. JSON body should include a `relationships` field with `[user_id, membership_level]` tuples.

NOTE: This replaces the membership list. If you leave off a project, the user will be REMOVED from that project. If the user was already a member of a project, their membership will be changed to the level specified. If the user was not previously a member of a project, they will be added with the level specified.

```
PUT /api/v1/projects/:id/project_members
```

This API call updates the project's membership list. JSON body should include a `relationships` field with `[user_id, membership_level]` tuples.

NOTE: This updates the membership list. If you leave off a project, the user’s relationship to that project will be unchanged. If the user was already a member of a project, their membership will be changed to the level specified. If the user was not previously a member of a project, they will be added with the level specified.

## Remove
```
DELETE /api/v1/projects/:id/project_members
```
This API call removes users from the project's membership list. JSON body should include a `user_ids` field, which is an array of `[user_id, user_id, ...]`.