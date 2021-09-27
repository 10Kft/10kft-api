# Staging vs. Production Environments

We provide a development environment called **`vnext`** so you can test out the API and develop your applications before going live with them in production. It is a staging environment completely isolated from your active account. We strongly encourage that you setup a test account on `vnext` and build your integrations there before moving to production.

There is no additional charge for maintaining a test account on vnext.

### How do I access the staging environment?

* Visit [`https://www.smartsheet.com/platform/10000ft/api-sandbox`](https://www.smartsheet.com/platform/10000ft/api-sandbox) to setup a test account.
* The API end point base URL for `vnext` is `https://vnext-api.10000ft.com/api/v1/`
* To access your test account, visit `https://vnext.10000ft.com` and sign in with your test account credentials.
* For support on vnext integration, contact us via our [Support Page](https://help.smartsheet.com/contact/resource-management)

### What changes when moving my integration to production?

* Your production account is your live Resource Management by Smartsheet Plans account available at `https://app.10000ft.com`
* The API end point base URL is `https://api.10000ft.com/api/v1/`
* You will use a production API token obtained from the settings section in your production account.
