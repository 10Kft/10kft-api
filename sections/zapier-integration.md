# 10,000ft Zapier Integration

Zapier is a web automation service that lets you integrate 10,000ft with thousands of other apps. You can read more details on the 10,000ft + Zapier [integrations page](https://zapier.com/apps/10000ft/integrations). 

## Requirements

* A 10,000ft account 
  * A 10,000ft API Token accessible via settings in your account
* A Zapier account
* Optionally, an account with each service that will be connected with 10,000ft via Zapier

Zapier provides free and paid plans. See the [Zapier pricing page](https://zapier.com/app/pricing) for more info.

## Configuring a Zap

Configuring a 10,000ft Zap typically involves,

* Connecting your 10,000ft account with Zapier
* Selecting a 10,000ft trigger
* Optionally, configure one or more Search steps to look up additional details
  * 10,000ft Triggers typically return user or assignable IDs
  * We provide find actions so you can get additional details (e.g. a user's email address) given their ID
  * This allows you to combine attributes you get from the trigger with additional attributes you get via searching to create Zaps that are rich in details and provide higher value.
* Choosing an app to connect with (e.g. Email)
* Configure, test and enable your Zap

## Example: Send an email when a new assignment is made in 10,000ft

Lets try a specific example. In the steps below we will make a Zap that will send an email to when one of your team members are assigned to a project. When you are done, this is what the outline of your Zap will look like,

  <img src="../assets/make-a-zap/overview.png" alt="overview" width="480">

And here are the steps in detail,

* Sign in to your Zapier account
* Start a Zap
* Search for the 10,000ft app and select it
* Select a 10,000ft Trigger (e.g. New Assignment)
  
  <img src="../assets/make-a-zap/1.png" alt="new assignment trigger" width="480">

* Connect your 10,000ft app if prompted by supplying your 10,000ft API token
* Add a step to search 10,000ft and lookup details for the user_id in the assignment
  
  <img src="../assets/make-a-zap/6.png" alt="find user by id options" width="480">

  * Add a step and select 10,000ft as the app
  * Search and select the `Find User by ID` action
  * Configure it to find the user for the `user_id` from the New Assignment trigger we setup above
  
* Add a step to search 10,000ft and lookup details for the assignable_id in the assignment
  * Add a step and select 10,000ft as the app
  * Search and select the `Find Assignable by ID` action
  * Configure it to find the assignable for the `assignable_id` from the New Assignment trigger we setup above
* Add a step to send an email
  
  <img src="../assets/make-a-zap/email-template-options.png" alt="email template options" width="480">

  * Select the Email by Zapier app
  * Configure it to send an email to user in the New Assignment
  * When you are done, the email template will look like this,
  

* Test and enable your Zap.

Now, everytime a new assignment is made on the 10,000ft schedule, the person who was added to the schedule will be sent an email with the name of the Project (or Leave) that they were assigned to and the start date of that assignment.

## Connecting 10,000ft with Zapier

  * This step is only required when connecting 10,000ft with your Zapier account for the first time
  * Add the 10,000ft API Token into Zapier when prompted, test and save your connection.


