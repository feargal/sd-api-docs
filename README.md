Server Density API
===
The [Server Density](http://www.serverdensity.com) API is implemented over simple HTTP with JSON responses authenticated using basic HTTP auth. It allows you to manage most aspects of the service including retrieving your historical server monitoring data, current status and post back data to us without needing the agent.

Clients
--
* PHP - [Server Density API](https://github.com/andrew-waters/Server-Density-API) (Andrew Waters)
* Python - [py-serverdensity](http://pypi.python.org/pypi/py-serverdensity/) (Wes Mason)

Methods
--
* [Alerts](sd-api-docs/blob/master/docs/alerts.md)
* Devices
* Metrics
* MongoDB
* Processes
* Services
* Users

Endpoint
--
All requests go through `https://api.serverdensity.com`. You can also access without SSL, although this is not recommended.

Versioning
--
All requests must access a specific API version, which is appended to the URL e.g. `https://api.serverdensity.com/1.4/`. 

See the [Release Notes](sd-api-docs/blob/master/docs/release-notes.md) for changes to the API. New versions will be announced on the [Server Density blog](http://blog.serverdensity.com).

Authentication
--
Authentication is through Basic HTTP Auth against your Server Density account. Each user has the same [permissions](http://support.serverdensity.com/knowledgebase/articles/76040-permissions) with access to the same devices and services as they do through the web UI.

**Enable the API for a user**

1. Log into your Server Density account
2. Click the Users tab then click Edit next to the user you wish to enable access for.
3. Tick the Enable API box and clik the Save changes button.

**Example**

    https://username:password@api.serverdensity.com/1.4/alerts/list?account=llama.serverdensity.com

**API keys**

We used to require a separate registration to obtain an API key in order to access the API. This proved to be unncessarily complicated so we have removed the need for keys and separate developer accounts.