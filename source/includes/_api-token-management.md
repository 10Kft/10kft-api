# API Token Management

Resource Management by Smartsheet API Tokens are used to authenticate requests to Resource Management by Smartsheet APIs. Organizations can manage up to 20 API tokens. Contact us via our [Support Page](https://help.smartsheet.com/contact/resource-management) if API Token Management is not enabled for your organization. The first generated token for an organization will have a set "primary" title.

## Get tokens

Returns list of tokens for your organization.

### Endpoint

`GET /api/api_tokens`

### Sample Response

```
[
    {
        "id": 1,
        "title": "primary",
        "token": <token_string>
    },
    {
        "id": 2,
        "title": "secondary",
        "token": <token_string>
    },
    {
        "id": 3,
        "title": null,
        "token": <token_string>
    }
]
```

## Create token

Create additional tokens for your organization.

### Endpoint

`POST /api/api_tokens`

### Optional Query Parameter

| **Name** | **Description**                                |
| -------- | ---------------------------------------------- |
| title    | an identifier for a token, cannot be "primary" |

## Delete token

Deletes the given token.

### Endpoint

`DELETE /api/api_tokens/<id>`

## Renew token

Deletes the given token and creates a new token.

### Endpoint

`POST /api/api_tokens/renew/<id>`

## Update token title

Update the title of the given token.

### Endpoint

`PUT /api/api_tokens/<id>`

### Query Parameter

| **Name** | **Description**                                |
| -------- | ---------------------------------------------- |
| title    | an identifier for a token, cannot be "primary" |
