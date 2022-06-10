# Webhooks

##### Endpoint: `/api/v1/webhooks`

Webhooks allow users to register, via the API, a webhook
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

curl 'https://api.rm.smartsheet.com/api/v1/webhooks?&auth=..'
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
      "url":"https://hooks.example.com/process_webhooks",
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

To prevent repetitive posting of the same webhook payload, no more than 10 webhooks per event type are permitted.

## Webhook Payloads

When a webhook is registered for a particular event type with the Resource Management by Smartsheet API,
every time an event of that type occurs, a POST is made to the webhook URL containing
data about the affected object. For example, if a webhook is registered for the project.created
event, every time a new project is created, a POST with the details of the created project is made to the
webhook's URL. This POST data is known as the webhook payload. A webhook payload looks like this:

```
{
    "data": {
      [ data about the object]
    },
    "type": [event type]
}
```
The "type" field indicates what type of event occurred, and is always one of the event types listed above.
The "data" field is exactly the same as what would be returned if the actual object
were fetched through the API via a GET call. Refer to the [Projects](#projects), [Users](#users),
[Time Entries](#time-entries) and [Assignments](#assignments) documentation for the exact format and return values
for the GET output. The data is exactly the same as a simple GET call output, with no additional fields
requested. It is not possible to request additional fields in the webhook payload, e.g. to request custom field values
or bill rates or other data that can be requested through the 'fields' parameter in typical API calls. If such additional
data is needed when processing a webhook, it is recommended that you make a GET request using the object ID returned in
the webhook payload, and specify any additional fields there.

### When do Updated Events fire?

Some of our data types, such as projects and users, are fairly complex and have other 'associated' data types such as bill rates, custom fields, etc. that are not direct properties of the object itself. We explain here what types of changes will cause updated events to trigger. Note that when an updated event fires, the payload is the same as a created event i.e. it contains data describing the object, but no specific information as to what changed. In the future, more information may be added, but currently, it is not supported.

#### Assignments

For assignments, any permitted change to an assignment (dates, allocation mode, percent, etc.) will trigger an updated event. **Note: Changing the assignee will trigger an `assignment.deleted` followed by an `assignment.created` event. We handle assignee changes differently than other attributes internally.**

#### Time Entries

For time entries, any permitted change such as (hours, notes, etc.) will trigger an updated event.

#### Projects

For projects, the following changes will trigger update events.

- Basic project property changes: name, start date, end date, project type, etc.

The following changes do *not* trigger updated events.

- Creating assignments for users on a project (though these are reported as assignment events)
- Changing or adding project budgets
- Changing or adding project bill rates
- Adding/editing tags or custom fields to a project
- Adding or change project custom fields

Some of these triggers do not exist yet because this is a newer feature. We expect update support to improve.
Adding phases to a project does trigger an event, but it is a separate event for phase creation, not a project update event (see the section on phases below).

#### Phases

While separate webhooks for phase events do not exist, phase create and update events will be reported on
project.created and project.updated webhooks.

#### Users

For users, the following changes will trigger update events.

- Basic property changes: name, email, etc.
- Role, discipline and location changes
- Availability and bill rate changes
- Tag and custom field changes

The following changes do *not* trigger updated events.

- Creating assignments for users on a project (though these are reported as assignment events)

## What should you return from your webhook processing code?

Resource Management by Smartsheet keeps track of return values from webhook processing code, and if a webhook is behaving poorly e.g. consistently
unreachable or in error, it may be automatically unsubscribed. Further, returning a 410 code on a webhook will also automatically unsubscribe it.

## Can Webhooks be viewed or edited from the application front-end?

At the moment there is no front end support for webhooks, they exist only as an API feature.






