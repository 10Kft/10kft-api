# Tags per Project

##### Endpoint: `/api/v1/projects/<project_id>/tags`

There are two ways to list project tags:

*   Get a list of tags for a single project using the `/api/v1/projects/<project_id>/tags` endpoint.
*   Adding the parameter `fields=tags` when listing/viewing through `/api/v1/projects`

## Create and attach tags to projects

Attaching a tag to a project is technically a "find-or-create" operation. If you post a tag with information that does not exist for your organization it will be created and attached to the project specified. If the tag already exists, it will just be attached. If you try to create the same tag multiple times, it will just be attached once.

```
curl -d "value=Awesome"  "https://api.rm.smartsheet.com/api/v1/projects/1/tags?auth=..."
```

## Disconnect a tag from a project

You can remove a tag from a project without deleting it from your account settings by using the /api/v1/projects endpoint.

```
curl -XDELETE  "https://api.rm.smartsheet.com/api/v1/projects/1/tags/456?auth=..."
```

## Response for Tags Listing

```
{
    "data": [
        {
            "id": 31,
            "value": "MyFirstTag"
        }
    ],
    "paging": {
        "next": null,
        "page": 1,
        "per_page": 20,
        "previous": null,
        "self": "/api/v1/projects/1/tags?project_id=1&per_page=20&page=1"
    }
}
```
