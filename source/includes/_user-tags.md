# Tags per User

##### Endpoint: `/api/v1/users/<user_id>/tags`

There are two ways to list user tags:

*   Get a list of tags for a single user using the `/api/v1/user/<user_id>/tags` endpoint.
*   Adding the parameter `fields=tags` when listing/viewing through `/api/v1/users`

## Create and attach tags to users

Attaching a tag to a user is technically a "find-or-create" operation. If you post a tag with information that does not exist for your organization it will be created and attached to the user specified. If the tag already exists, it will just be attached. If you try to create the same tag multiple times, it will just be attached once.

```
curl -d "value=Awesome"  "https://api.rm.smartsheet.com/api/v1/users/1/tags?auth=..."
```

## Disconnect a tag from a user

You can remove a tag from a user without deleting it from your account settings by using the /api/v1/users endpoint.

```
curl -XDELETE  "https://api.rm.smartsheet.com/api/v1/users/1/tags/456?auth=..."
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
        "self": "/api/v1/users/1/tags?user_id=1&per_page=20&page=1"
    }
}
```
