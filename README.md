# 10,000ft API (Pro, Enterprise and Business plans)

The 10,000ft API provides programmatic access to projects, users and time entries in your account, commonly referred to as _resources_ in the rest of this API documentation. The API implements a standard HTTP REST pattern and allows callers with appropriate authentication and authorization to programmatically create, read, update and delete these resources.

API access is available on Pro, Enterprise and Business plans of 10000ft. As of June 2019, all new plans purchased are Business, and include API access. For customers prior to this date, API access is based on your current plan.

# Overview

* [General information](sections/first-things-first.md) (read first)
  * [Collections & Objects](https://github.com/10Kft/10kft-api/blob/master/sections/first-things-first.md#collections--objects)
  * [Pagination](https://github.com/10Kft/10kft-api/blob/master/sections/first-things-first.md#pagination)
  * [Authentication](https://github.com/10Kft/10kft-api/blob/master/sections/first-things-first.md#authentication)
  * [Optional Fields](https://github.com/10Kft/10kft-api/blob/master/sections/first-things-first.md#optional-fields)
  * [Date/Time Formatting](https://github.com/10Kft/10kft-api/blob/master/sections/first-things-first.md#date--time-formatting)
  * [Error Handling](https://github.com/10Kft/10kft-api/blob/master/sections/first-things-first.md#error-handling)
  * [Throttling/Rate-limiting](https://github.com/10Kft/10kft-api/blob/master/sections/first-things-first.md#throttling--rate-limiting)
* [How to setup a staging environment for testing](sections/staging-environment.md)

# Need help?

* Contact us via our [Support Page](https://help.smartsheet.com/contact?contactType=10k-support)
  * Read more on how to report a problem [here](sections/getting-help.md).
* Have a suggestion for improving our API documentation? Send us a pull-request or email support.

# Endpoints

The API provides access to the following data collections in your account via RESTful endpoints.

* [Users](sections/users.md)
  * [User Tags](sections/user-tags.md)
  * [Availabilities](sections/user-availabilities.md)
* [Placeholder Resources](sections/placeholders.md)
* [Projects](sections/projects.md)
  * [Users by Project](sections/project-users.md)
  * [Project Tags](sections/project-tags.md)
  * [Phases](sections/phases.md)
* [Project Budgets](sections/budget-items.md)
* [Leave Types](sections/leave-types.md)
* [Time Entries](sections/time-entries.md)
* [Expense Items](sections/expense-items.md)
* [Assignments](sections/assignments.md)
* [Subtasks](sections/subtasks.md)
* [Bill Rates](sections/bill-rates.md)
* [Statuses](sections/user-statuses.md) (_deprecated_)
* [Time & Expense Approvals](sections/approvals.md)
* [Holidays](sections/holidays.md)
* [Custom Fields](sections/custom-fields.md)
* [Reports](sections/reports.md)
* [Status Options](sections/status-options.md)
* [Assignables](sections/assignables.md)


# Webhooks (New!)

The 10,000ft API now supports webhooks for certain events. See [the webhooks page](sections/webhooks.md) for details.

# Zapier Integration

Our Zapier integration helps you integrating with the 10,000ft API in convenient and powerful ways and connect many other apps and services used by yor team.

* [10,000ft on Zapier](https://zapier.com/apps/10000ft/integrations)
* [Getting started with Zapier](sections/zapier-integration.md)

# Case studies

Some case studies of our customers using our API to build new tools and applications using the 10Kft API.

  * [Fancy Pants Group](https://www.10000ft.com/blog/fancy-pants-group-case-study), a digital creative studio based in New York, recently used our API to develop and launch a custom project importer cheekily called Job the Builder. Their goal is to make it easy for everyone on their 100-person team to see and communicate consistent data across multiple tools.

# Third party libraries

A few of our customers have implemented and shared API client libraries to help using the 10Kft API easier. Depending on your scenario, you may benefit from adopting and improving on them. Here are a couple of references,

* Revelry Labs / `ruby` / https://github.com/revelrylabs/tenk
* Spindance / `ruby` / https://github.com/spindance/ten_thousand_feet
* Work & Co / `go` / https://github.com/workco/go-tenkft

# Questions?

Questions or feedback about our API, please submit a support ticket at our [Support Page](https://help.smartsheet.com/contact?contactType=10k-support) 
