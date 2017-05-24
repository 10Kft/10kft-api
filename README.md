# 10,000ft API

The 10,000ft API provides programmatic access to projects, users and time entries in your account, commonly referred to as _resources_ in the rest of this API documentation. The API implements a standard HTTP REST pattern and allows callers with appropriate authentication and authorization to programmatically create, read, update and delete these resources.

# Overview

* [General information](sections/first-things-first.md) (read first)
* [How to get help or report a problem](sections/getting-help.md)
* [How to setup a staging environment for testing](sections/staging-environment.md)

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
* [Time Entries](sections/time-entries.md)
* [Assignments](sections/assignments.md)
* [Bill Rates](sections/bill-rates.md)
* [Statuses](sections/user-statuses.md) (_deprecated_)
* [Time & Expense Approvals](sections/approvals.md)
* [Holidays](sections/holidays.md)


## Pro & Enterprise Only

* [Custom Fields](sections/custom-fields.md)

## Third party libraries

A few of our customers have implemented and shared API client libraries to help using the 10Kft API easier. Depending on your scenario, you may benefit from adopting and improving on them. Here are a couple of references,

* Revelry Labs / `ruby` / https://github.com/revelrylabs/tenk
* Spindance / `ruby` / https://github.com/spindance/ten_thousand_feet
* Work & Co / `go` / https://github.com/workco/go-tenkft

# Questions?

Please don't hesitate to reach out to us via the in-app support feature for questions or suggestions about using the 10,000ft API. We're here to help.
