Any changes and updates to the API will be noted here. Major releases will be announced on the [Server Density blog](http://blog.serverdensity.com).

1.4.3 (26 July 2012)
---
* New `alerts/add` and `alerts/delete` methods.

1.4.2 (15 June 2012)
---
* `services/list` method now returns the last check information for each region and takes an optional `regionsInfo` parameter to return meta data about each region (name, city, country, provider and co-ordinates).

1.4.1 (5th April 2012)
---
* New functions - `users/addEmail`, `users/addPhone`, `users/deleteEmail`, `users/deletePhone`
* New functions - `devices/count`
* `devices/list` now accepts `limit` and `skip` parameters

1.4.0 (10th Jan 2012)
---
New API 1.4 released. 1.3 deprecated.

* `devices/rename` is now a POST method instead of a GET method.
* `users/delete` is now a POST method instead of a GET method.
* `metrics/getRange` now uses a new request and response format and offers metrics at 1 minute granularity.

1.3.1 (19th Oct 2011)
---
* New function - `users/list`

1.3.0 (29th Aug 2011)
---
New API 1.3 released. 1.0, 1.1 and 1.2 deprecated.

* New function - `metrics/postback`
* New URL schema and authentication changes requiring a developer key with rate limiting defauling to 2 queries per second.

1.2.1 (19th Jul 2011)
---
* New functions - `servers/rename` and `servers/getByName`

1.2.0 (16th Jun 2011)
---
New 1.2 API released. 1.1 API deprecated.

* New functions - `alerts/getOpenNotified`, `mongo/getMaster`, `mongo/getReplicaSet`, `processes/getRange`, `processes/getByTime`

1.1.0 (25th Nov 2010)
---
New 1.1 API released. 1.0 API deprecated.

* IDs are now strings rather than integers. The old integer ID is provided where appropriate but cannot be used for queries.

1.0.14 (17th Aug 2010)
---
* Fix problem where some timestamps could be output in non-standard format. Now ensures ISO 8601 e.g. `2010-08-17T10:21:13+0000`. Units will now also be output for most metrics as a separate field. 

1.0.13 (24th January 2010)
---
* Added `users/getbyip function`. No endpoint version update needed.

1.0.12 (8th November 2009)
---
* `ip` parameter for `servers/add` is now optional.

1.0.11 (2nd November 2009)
---
* Added `metrics/getmysqlstatus` and `metrics/getmysqlstatusrange` functions.

1.0.10 (24th October 2009)
---
* Added `servers/delete` and `users/delete` functions. 
* Added optional email parameter to `users/add function`

1.0.9 (20th October 2009)
---
* Added `metrics/getnginxstatus` and `metrics/getnginxstatusrange` functions.

1.0.8 (4th October 2009)
---
* Added `servers/addgroup` and `users/add` functions. Only admin users can now add servers. 

1.0.7 (27th September 2009)
---
* Added `mountedOn` parameter to `metrics/getdiskusagerange` to limit returned data to a specific mount point. 

1.0.6 (3rd September 2009)
---
* Added new server functions `servers/getbygroup`, `servers/listgroups`, added server group output where server information returned, added username and admin to user details output for `alerts/list` and `alerts/getlatest` and apply permissions to API output.

1.0.5 (4th August 2009)
---
* Added new server function `servers/add`

1.0.4 (3rd July 2009)
---
* Convert `timeAlerted` for `alerts/getlatest` to user timezone. `timeAlertedGMT` added for GMT time.

1.0.3 (1st July 2009)
---
* All functions now round output values to 2DP or 0DP where appropriate.

1.0.2 (28th June 2009)
---
* Added new iPhone functions - `iphone/setdevicetoken` for upcoming push notification support.

1.0.1 (27th June 2009)
---
* Added new network traffic metric functions - `metrics/getnetworktraffic` and `metrics/getnetworktrafficrange`

1.0.0 (11th June 2009)
---
First release.