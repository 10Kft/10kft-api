# Subtasks
##### Endpoint: `/api/v1/projects/<project_id>/assignments/<assignment_id>/subtasks`
Subtasks belong to assignments. They correspond to the checklist of items called a `tasklist` listed under work items/assignments in the worklist. Tasks are an optional addition to any work item/assignment.
## Create a subtask
```
POST /api/v1/projects/<project_id>/assignments/<assignment_id>/subtasks
```
##### Required params
| param       | description |
| ----------- | ----------- |
| description | string used to describe the subtask |
##### Optional params
| param       | description |
| ----------- | ----------- |
| completed   | boolean value that corresponds with checkbox, default false |
##### Example
```
POST {
  "description": "Create wireframe",
  "completed": true,
}
```
## List subtasks
```
GET /api/v1/projects/:project_id/assignments/:assignment_id/subtasks
```
## Show a single subtask
```
GET /api/v1/projects/:project_id/assignments/:assignment_id/subtasks/<subtask_id>
```
## Update a subtask
```
PUT /api/v1/projects/:project_id/assignments/:assignment_id/subtasks/<subtask_id>
```
## Delete a subtask
```
DELETE /api/v1/projects/:project_id/assignments/:assignment_id/subtasks/<subtask_id>
```
Deleting a subtask will permantently destroy the record. For updates to subtasks we record the user_id of the last update and the time of the last update.
