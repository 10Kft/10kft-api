# 10,000ft API (Pro and Enterprise only)

The 10,000ft API provides programmatic access to projects, users and time entries in your account, commonly referred to as _resources_ in the rest of this API documentation. The API implements a standard HTTP REST pattern and allows callers with appropriate authentication and authorization to programmatically create, read, update and delete these resources.

API access is available only on Pro and Enterprise plans of 10000ft.

# Overview

* [General information](sections/first-things-first.md) (read first)
* [How to setup a staging environment for testing](sections/staging-environment.md)

# Need help?

* Email questions to support@10000ft.com
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
* [Leave Types](sections/leave-types.md)
* [Time Entries](sections/time-entries.md)
* [Assignments](sections/assignments.md)
* [Bill Rates](sections/bill-rates.md)
* [Statuses](sections/user-statuses.md) (_deprecated_)
* [Time & Expense Approvals](sections/approvals.md)
* [Holidays](sections/holidays.md)
* [Custom Fields](sections/custom-fields.md)
* [Reports](sections/reports.md)
* [Webhooks](sections/reports.md) *New*

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

Please don't hesitate to reach out to us via the in-app support feature for questions or suggestions about using the 10,000ft API. We're here to help.
