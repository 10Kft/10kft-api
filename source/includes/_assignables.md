
# Assignables

##### Endpoint: `/api/v1/assignables`
An _assignable_ in Resource Management by Smartsheet Plans is an object to which an assignment can be made, i.e. a person, placeholder, etc. can be assigned to this object. Currently, there are two types of assignables in Resource Management by Smartsheet Plans, [Projects](#projects) and [Leave Types](#leave-types). Phases are also an assignable, but they can be accessed through the [projects endpoint](#projects).

It is useful to have an understanding of Assignables as an API entity because the [Assignments endpoint](#assignments) returns an _assignable-id_ to indicate the object to which the assignment is made, but without knowing the _type_ of that object, it is not clear which endpoint to use to get more details about the object if desired. The assignables endpoint allows you to query directly using the `assignable-id` from an assignment.

The endpoint supports two actions, index and show. It is not possible to create a generic assignable or to delete one, the Projects/LeaveTypes endpoints should be used for those actions.

## List Assignables (index)

```
GET  /api/v1/assignables

 curl 'https://api.rm.smartsheet.com/api/v1/assignables?auth=...'
```

## Show an Assignable

```
GET  /api/v1/assignables/<assignable-id>

 curl 'https://api.rm.smartsheet.com/api/v1/assignables/12345?auth=...'
```

## Return values based on type

The format returned by this endpoint depends on the type of the object returned. If a project, the return value will look exactly like what is returned by the [Projects endpoint](#projects), and if a LeaveType, the return value looks exactly like what is returned by the [LeaveTypes endpoint](#leave-types). In both cases, the return value has a _type_ property, which will be _Project_ or _LeaveType_, respectively (phases also have the type _Project_).

## Sample Response

```
{
"paging":
	{
		"per_page":20,
		"page":1,"previous":null,
		"self":"/api/v1/assignables?&page=1",
		"next":null
	},
"data": [
	{
 		"id":1,
		"description":null,
		"guid":"bd5fa048-b3f4-467a-a3b5-18211d488d21",
		"name":"Vacation",
		"deleted_at”:null,
		"type":"LeaveType",
	},
	{
		"id":4,
		"description":null,
		"guid":"76c4d8d0-4351-4842-8da2-de715d3a37e5",
		"name":"Project A",
		"deleted_at":null,
		"type":"Project",
		"starts_at":"2018-09-15",
		"ends_at":"2018-09-19",
		"parent_id":null,
		"phase_name":null,
		"thumbnail":null,
		"project_code":"",
		"timeentry_lockout":-1,
		"client":""
	}]
}
```
