# Resource Management by Smartsheet Zapier Integration

Zapier is a web automation service that lets you integrate Resource Management by Smartsheet with thousands of other apps. You can read more details on the Resource Management by Smartsheet + Zapier [integrations page](https://zapier.com/apps/10000ft/integrations).

## Requirements

* A Resource Management by Smartsheet account
* A Zapier account
* Optionally, an account with each service that will be connected with Resource Management by Smartsheet via Zapier

Zapier provides free and paid plans. See the [Zapier pricing page](https://zapier.com/pricing) for more info.

## Connecting Resource Management by Smartsheet with Zapier

  * This step is only required when connecting Resource Management by Smartsheet with your Zapier account for the first time
  * Start by making a new Zap in your Zapier account
  * Find the Resource Management by Smartsheet app and pick any trigger to initiate the setup
  * When prompted, add the Resource Management by Smartsheet API Token into Zapier, test and save your connection

    <img src="images/make-a-zap/3.png" alt="add API token" width="480">

Once the connection is setup and tested, you can use it to make new Zap. Lets go through the steps and setup an example Zap.

## Configuring a Zap

Configuring a Resource Management by Smartsheet Zap typically involves,

* Connecting your Resource Management by Smartsheet account with Zapier
* Selecting a Resource Management by Smartsheet trigger
* Optionally, configure one or more Search steps to look up additional details
  * Resource Management by Smartsheet Triggers typically return user or assignable IDs
  * We provide find actions so you can get additional details (e.g. a user's email address) given their ID
  * This allows you to combine attributes you get from the trigger with additional attributes you get via searching to create Zaps that are rich in details and provide higher value.
* Choosing an app to connect with (e.g. Email)
* Configure, test and enable your Zap

## Example: Send an email when a new assignment is made in Resource Management by Smartsheet

Lets try a specific example. In the steps below we will make a Zap that will send an email to when one of your team members are assigned to a project. When you are done, this is what the outline of your Zap will look like,

  <img src="images/make-a-zap/overview.png" alt="overview" width="480">

And here are the steps in detail,

* Sign in to your Zapier account
* Start a Zap
* Search for the Resource Management by Smartsheet app and select it
* Select a Resource Management by Smartsheet Trigger (e.g. New Assignment)

  <img src="images/make-a-zap/1.png" alt="new assignment trigger" width="480">

* Connect your Resource Management by Smartsheet app if prompted by supplying your Resource Management by Smartsheet API token
* Add a step to search Resource Management by Smartsheet and lookup details for the user_id in the assignment

  <img src="images/make-a-zap/6.png" alt="find user by id options" width="480">

  * Add a step and select Resource Management by Smartsheet as the app
  * Search and select the `Find User by ID` action
  * Configure it to find the user for the `user_id` from the New Assignment trigger we setup above

* Add a step to search Resource Management by Smartsheet and lookup details for the assignable_id in the assignment
  * Add a step and select Resource Management by Smartsheet as the app
  * Search and select the `Find Assignable by ID` action
  * Configure it to find the assignable for the `assignable_id` from the New Assignment trigger we setup above
* Add a step to send an email

  <img src="images/make-a-zap/email-template-options.png" alt="email template options" width="480">

  * Select the Email by Zapier app
  * Configure it to send an email to user in the New Assignment
  * When you are done, the email template will look like this,

* Test and enable your Zap.

Now, when a new assignment is made on the Resource Management by Smartsheet schedule, the person who was assigned will be sent an email with the name of the Project (or Leave) that they were assigned to and the start date of that assignment.

## Filters & additional considerations

Zapier Filters are useful when building integrations with Resource Management by Smartsheet. You can use any attribute from a trigger of search action when implementing a filter. The `Type` attribute available in Resource Management by Smartsheet users and assignabled are particularly useful. For example, in the example above your Zap would typically exclude Placeholder users. This would be implemented by adding a FIlter to you Zap as shown below.

  <img src="images/make-a-zap/filter-options.png" alt="email filter options" width="480">

Familiarize yourself with the different types of users and assignables available in Resource Management by Smartsheet when designing your Resource Management by Smartsheet Zaps so you can get the result you are trying to achive with your integration. See [Resource Management by Smartsheet API documentation](#Resource Management by Smartsheet-api-(pro-and-enterprise-only)) for more details on specific attributes.

## Triggers

Resource Management by Smartsheet provides the following Triggers

* **New Assignment** Triggers when a new assignment is created.
* **New User** Triggers when a new user is created.
* **New Project** Triggers when a new project gets created.
* **New Time Entry** Triggers when a new time entry is created.
* **Assignment Updated** Triggers when an assignment is updated.
* **User Updated** Triggers when a new user is updated.
* **Project Updated** Triggers when a project gets updated.
* **Time Entry Updated** Triggers when a new time entry is updated.

## Actions

Resource Management by Smartsheet provides the following actions for creating or updating information in your Resource Management by Smartsheet account via Zapier

* **Create Project** Create a new project.
* **Create User** Create a new team member.
* **Create Time Entry** Create a new time entry.
* **Update Project** Updates a project.
* **Update User** Updates a team member.
* **Update Time Entry** Update a time entry.

## Searches

* **Find Assignable by ID** Finds an existing assignable by the assignable's ID. An assignable is anything that can be assigned to a user such as a Project or Leave type.
* **Find Project by ID** Finds an existing project using the project's ID.
* **Find User by ID** Finds an existing user by their ID.
* **Find User by Email** Finds an existing user by their email.
* **Find User by Name** Finds an existing user by their name.
* **Find Assignable by Name** Finds an existing assignable by name.
* **Find Project by Name** Finds an existing project by name.

## More details about the Resource Management by Smartsheet API

Zapier is a convenient and powerful way to consume the Resource Management by Smartsheet API. The triggers, actions and searches listed above allow you to access commonly used API functionality without having to develop custom API integrations or write software code.

The Resource Management by Smartsheet API provides access to a number of advanced features that are not currently supported with our Zapier triggers and actions.

Have a question? Contact us via our [Support Page](https://help.smartsheet.com/contact/resource-management). We are here to help!









