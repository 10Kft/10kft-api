# Webhooks (New!)

##### Endpoint: `/api/v1/webhooks`

The webhooks feature allows users to register, via the API, a webhook 
that they can use to receive notifications about key events in their account.
Currently, webhooks are supported for the following events.


| **Event Type** | **Description** |
| ------------- | --------------- |
| project.created | fires when a new project is created |
| project.updated | fires when a project is updated |
| time.entry.created | fires when a new time entry is created |
| time.entry.updated | fires when a time entry is updated |
| user.created | fires when a new time entry is created |
| user.updated | fires when a user is updated |
| assignment.created | fires when a new assignment is created |
| assignment.updated | fires when an assignment is updated |


## List Webhooks

```
GET /api/v1/webhooks
```

Lists all the webhooks for your organization.


#### Example

```
GET /api/v1/webhooks/

curl 'https://vnext.10000ft.com/api/v1/webhooks?&auth=..'
```

#### Response

```
{
  "paging": {
   ...  
  },
  "data": [
    {
      "id":1,
      "organization_id":1,
      "url":"https://10000ft.com/process_webhooks",
      "status":"active",
      "event_type":"project.created"
    }
  ]
}
```

#### Response Fields

**Field** | **Description** |
| ------------- | --------------- |
| id | unique identifier for the webhook |
| organization_id | unique identifier for the organization to which the webhook belongs |
| url | url associated with the webhook, to which events are posted |
| status | status of the webhook |
| event_type | type of event associated with the webhook |

#### Webhook Status

Currently, the only valid status for a webhook is 'active'. This field is reserved for future extensions of the webhooks API.


## Creating a webhook

```
POST /api/v1/webhooks
```

##### Required parameters:

| **Parameter** | **Description** |
| ------------- | --------------- |
| event_type | type of event associated with the webhook |
| url | url to which events should be posted |

Both parameters are required. The 'event_type' must be one of the supported types mentioned above. 
The url must be https with a valid host.

## Deleting a webhook

```
DELETE /api/v1/webhooks/<webhook_id>
```

## Updating a webhook

This is currently not permitted.

## Webhook Limits

A limit of 10 webhooks per event type per account is enforced. If more webhooks are needed, we recommend
that the webhook processing logic be consolidated at a single endpoint.

## Webhook Payloads

When a webhook is registered for a particular event type with the 10000ft API, 
every time an event of that type occurs, a POST is made to the webhook URL containing
data about the affected object. For example, if a webhook is registered for the project.created
event, every time a new project is created, a POST with the details of the created project is made to the
webhook's URL. The data contained in this POST is exactly the same as what would be returned if the actual object
were fetched through the API via a GET call. Refer to the [Projects](projects.md), [Users](users.md),
[Time Entries](time-entries.md) and [Assignments](assignments.md) documentation for the exact format and return values 
for the GET output. The webhook payload is exactly the same as a simple GET call output, with no additional fields 
requested. It is not possible to request additional fields in the webhook payload, e.g. to request custom field values
or bill rates or other data that can be requested through the 'fields' parameter in typical API calls. If such additional
data is needed when processing a webhook, it is recommended that you make a GET request using the object ID returned in
the webhook payload, and specify any additional fields there.

#### Phases

While separate webhooks for phase events do not exist, phase create and update events will be reported on 
project.created and project.updated webhooks.

#### Webhook return values

10000ft keeps track of return values from webhook processing code, and if a webhook is behaving poorly e.g. consistently 
unreachable or in error, it may be automatically unsubscribed. Further, returning a 410 code on a webhook will also automatically
unsubscribe it.








