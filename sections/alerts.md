Alerts
===
* [Add](#add) - adds a new alert.
* [Delete](#delete) - deletes a specific alert.
* [Get history](#get-history) - returns the full history for each time a specific alert has been triggered.
* [Get last](#get-last) - returns the last 5 triggered alerts across the whole account.
* [Get open](#get-open) - returns the current open, non-fixed alerts.
* [Get open notified](#get-open-notified)` - returns the current open, non-fixed alerts which have sent notifications.
* [List](#list) - returns all configured alerts.
* [Pause](#pause) - pauses a specific alert.
* [Resume](#resume) - resumes a specific alert.

Add
--
`POST /alerts/add`

Adds a new alert.

*Users can only add alerts for devices/services they have permission to access. If they are not an admin user they can only add alerts for themself.*

**Parameters - general**

* `userId[]` *array* - Array of one or more user IDs to be notified when this alert triggers. Use the `users/list` method and provide the numerical user ID from the `userIdOld` field. One of the array items can also be `pagerduty` if you wish to notify PagerDuty through our integration. To notify all members of the group the device/service belongs to, include `group` as one of the array items.
* `serverId` *string* or *int* - The ID for the device/service to create this alert for. For devices, the numerical ID from the `deviceIdOld` field when calling the `devices/list` method. For services, the 32 bit string from the `_id` field when calling the `services/list` method.
* `notificationType[]` *array* - Array of one or more notification types: 
    * `email`
    * `sms`
    * `iphonepush`
    * `androidpush`
* `checkType` *string* - One of the [check types](alerts-check-types.md).
* `comparison` *string* - The comparison for the alert threshold:
    * `<`
    * `<=`
    * `>`
    * `>=`
* `triggerThreshold` *int* - The threshold to trigger the alert, with the following exceptions
    * For the `noData` check type, this field is called `triggerThresholdMin` instead.
    * For the `httpNotResponding` check type, this field is called `triggerThresholdNodes` instead.
* `notificationFixed` *bool* - Whether to send a final notification when the triggered alert is fixed.

**Parameters - notification delay**

Specify one of these two fields to configure how long to wait after triggering the alert before notifications are sent:

* `notificationDelay` *int* - Number of minutes to wait.
* `notificationDelayImmediately` *bool* - Send notifications immediately. If this field is set, it will override `notificationDelay`.

**Parameters - notification frequency**

Specify one of these two fields to configure how often notifications are sent:

* `notificationFrequency` *int* - Number of minutes between each notification.
* `notificationFrequencyOnce` *bool* - Only send one set of notifications. If this field is set, it will override `notificationFrequency`.

**Parameters - check specific**

These parameters must also be provided for certain check types. Be sure to [read the support docs about dynamic metrics](http://support.serverdensity.com/knowledgebase/articles/75897-dynamic-dashboard-metrics) to understand how to provide the correct values.

* `cpuStatsDevice` *string - The name of the CPU for all CPU alerts.
* `diskUsageMountPoint` *string* - The name of the mount point or drive letter for `diskUsagePercent` alerts.
* `httpResponseString` *string* - The expected string for `httpResponseString` and `httpResponseStringNotPresent` alerts and the MD5 checksum for the `httpResponseStringMD5` check type.
* `ioStatsDevice` *string* - The i/o device name for all i/o stats alerts.
* `processName` *string* - The process name to match against for `processNotRunning` alerts. This will [either be an exact match or a regular expression](http://support.serverdensity.com/knowledgebase/articles/71126-process-not-running-alerts-exact-and-regex-match). Regexes will start and end with `/` and will be syntax checked.
* `queueName` *string* - Name of the queue for all RabbitMQ alerts.
* `pluginKey` *string* - The name of the key returned by the plugin.

**Request**

`https://api.serverdensity.com/1.4/alerts/add?account=example.serverdensity.com`

**Response**

```json
{
    "status": 1,
    "data": {
        "alertId": "4e7551da150ba0e8140009ae"
    }
}
```

**Example**

Creates an alert for user ID 1 and all users in the group the device ID 1 belongs to. It will be triggered when the disk usage on the root (/) volume is equal to or greater than 70% used. Notifications will be sent via e-mail and SMS immediately and then every 60 minutes. A final notification will be sent when the alert is fixed.

Note: For curl, the fields are URL encoded.

```bash
curl -v -O /dev/stdout --user USER "http://api.serverdensity.com/1.4/alerts/add?account=example.serverdensity.com" \
-d userId[]=group \
-d userId[]=1 \
-d serverId=1 \
-d notificationType[]=email \
-d notificationType[]=sms \
-d checkType=diskUsagePercent \
-d comparison=%3E%3D \
-d triggerThreshold=70 \
-d notificationFixed=true \
-d notificationDelayImmediately=true \
-d notificationFrequency=60 \
-d diskUsageMountPoint=%2F
```

Delete
--
```POST /alerts/delete```

Deletes a specific alert.

*Only admin users can use this method*

**Parameters**

* `alertId` *string* - You can find this value by calling the `list` method or looking at the ID at the end of the URLs for editing an alert in the web interface.

**Request**

`https://api.serverdensity.com/1.4/alerts/delete?account=example.serverdensity.com`

**Response**

```json
{
    "status": 1,
    "data": {
        "alertDeleted": 1
    }
}
```

Get history
--
`GET /alerts/getHistory`

Returns the full history for each time a specific alert has been triggered.

**Parameters**

* `alertId` *string* - You can find this value by calling the `list` method or looking at the ID at the end of the URLs for editing an alert in the web interface.

**Request**

`GET https://api.serverdensity.com/VERSION/alerts/getHistory?account=example.serverdensity.com&alertId=4f86b63aff4bb6fc03000015`

**Response**
```json
{
    "status": 1,
    "data": {
        "alerts": [
            {
                "alert": {
                    "alertId": {
                        "$id": "4f86b63aff4bb6fc03000015"
                    },
                    "timeAlertedGMT": "2012-06-08T10:37:16+00:00",
                    "alertTriggeredId": {
                        "$id": "4fd1d5dcd21be404a63395ac"
                    },
                    "fixed": 1,
                    "timeAlerted": "2012-06-08 10:37:16",
                    "timeAlertedText": "Jun 8th",
                    "timeFixedGMT": "2012-06-08T10:40:10+00:00",
                    "checkType": "noData",
                    "triggeredValue": "6 mins",
                    "notificationType": [
                        "email"
                    ],
                    "lastNotified": "2012-06-08 10:37:16",
                    "timestamp": null,
                    "timeFixed": "2012-06-08 10:40:10",
                    "checkTypeText": "No data received",
                    "notificationTypeText": "E-mail"
                },
                "users": [],
                "usersText": "PagerDuty Critical",
                "device": {
                    "serverId": 291,
                    "name": "a1.wdc.sl",
                    "cloudMonitoring": false
                }
            }
        ]
    }
}
```

Get last
--
`GET /alerts/getLast`

Returns the last 5 triggered alerts across the whole account.

**Request**

`GET https://api.serverdensity.com/1.4/alerts/getLast?account=example.serverdensity.com`

**Response**
```json
{
    "status": 1,
    "data": {
        "alerts": [
            {
                "alert": {
                    "alertId": "4fa4262a1212bac21b000045",
                    "timeAlertedGMT": "2012-07-04T10:45:28+00:00",
                    "checkType": "loadAvrg",
                    "triggeredValue": "2.58",
                    "notificationType": "email",
                    "fixed": "0",
                    "timeAlerted": "2012-07-04T11:45:28+00:00",
                    "timeAlertedText": "4 mins ago",
                    "checkTypeText": "System: Load average",
                    "paused": 0,
                    "notificationTypes": [
                        "E-mail"
                    ]
                },
                "users": [
                    {
                        "userId": "4b7094736593e1737c376633",
                        "userIdOld": 7,
                        "username": "pagerduty-noncritical",
                        "firstName": "PagerDuty",
                        "lastName": "Non-critical",
                        "admin": false
                    }
                ],
                "device": {
                    "serverId": "4f27c64cfe4bb6a16c00018c",
                    "serverIdOld": 260,
                    "name": "puppet",
                    "group": "",
                    "os": "linux"
                }
            },
            ...
        ]
    }
}
```

Get open
--
`GET /alerts/getOpen`

Returns the current open, non-fixed alerts.

**Request**

`https://api.serverdensity.com/1.4/alerts/getOpen?account=example.serverdensity.com`

**Response**

```json
{
    "status": 1,
    "data": {
        "alerts": [
            {
                "alert": {
                    "alertId": "4fa780b21212bade330001b7",
                    "timeAlertedGMT": "2012-05-08T12:00:20+00:00",
                    "timeLastNotifiedGMT": "2012-05-08T12:00:20+00:00",
                    "checkType": "processNotRunning",
                    "triggeredValue": false,
                    "notificationType": "email",
                    "fixed": "0",
                    "timeAlerted": "2012-05-08T13:00:20+00:00",
                    "timeAlertedText": "May 8th",
                    "checkTypeText": "Process not running (/(.*)s3-sync.sh/)",
                    "triggerThresholdText": "-",
                    "paused": 0,
                    "notificationTypes": [
                        "E-mail"
                    ]
                },
                "users": [
                    {
                        "userId": "4b7094736593e1737c376633",
                        "userIdOld": 7,
                        "username": "pagerduty-noncritical",
                        "firstName": "PagerDuty",
                        "lastName": "Non-critical",
                        "admin": false
                    }
                ],
                "device": {
                    "serverId": "4f27c64cfe4bb6a16c00018c",
                    "serverIdOld": 260,
                    "name": "puppet",
                    "group": "",
                    "os": "linux"
                }
            },
            ...
        ]
    }
}
```

Get open notified
--
`GET /alerts/getOpenNotified`

Returns the current open, non-fixed alerts which have sent notifications. This is contrasted with the [getOpen](#get-open) method which returns all open alerts whether or not notifications have been sent. Notifications might not yet have been sent if a delay is set up in the alert configuration.

**Request**

`https://api.serverdensity.com/1.4/alerts/getOpenNotified?account=example.serverdensity.com`

**Response**

```json
{
    "status": 1,
    "data": {
        "alerts": [
            {
                "alert": {
                    "alertId": "4fa780b21212bade330001b7",
                    "timeAlertedGMT": "2012-05-08T12:00:20+00:00",
                    "timeLastNotifiedGMT": "2012-05-08T12:00:20+00:00",
                    "timeAlerted": "2012-05-08T13:00:20+00:00",
                    "timeAlertedText": "May 8th",
                    "checkType": "processNotRunning",
                    "triggeredValue": "-",
                    "notificationType": "email",
                    "fixed": "0",
                    "checkTypeText": "Process not running (/(.*)s3-sync.sh/)",
                    "paused": 0,
                    "notificationTypes": [
                        "E-mail"
                    ]
                },
                "users": [
                    {
                        "userId": "4b7094736593e1737c376633",
                        "userIdOld": 7,
                        "username": "pagerduty-noncritical",
                        "firstName": "PagerDuty",
                        "lastName": "Non-critical",
                        "admin": false
                    }
                ],
                "device": {
                    "serverId": "4f27c64cfe4bb6a16c00018c",
                    "serverIdOld": 260,
                    "name": "puppet",
                    "group": "",
                    "os": "linux"
                }
            },
            ...
        ]
    }
}
```

List
--
`GET /alerts/list`

Returns all configured alerts.

**Request**

`https://api.serverdensity.com/1.4/alerts/list?account=example.serverdensity.com`

**Response**

```json
{
    "status": 1,
    "data": {
        "alerts": [
            {
                "alert": {
                    "alertId": "4f86de1d1212bac070000007",
                    "paused": "0",
                    "checkType": "diskUsagePercent",
                    "comparison": ">=",
                    "triggerThreshold": 80,
                    "checkTypeText": "System: Disk usage (\/var\/lib\/mongodb)",
                    "triggerThresholdText": "80%",
                    "notificationTypes": [
                        "E-mail"
                    ]
                },
                "users": [
                    {
                        "userId": "4b7094736593e1737c376633",
                        "userIdOld": 7,
                        "username": "pagerduty-noncritical",
                        "firstName": "PagerDuty",
                        "lastName": "Non-critical",
                        "admin": false
                    }
                ],
                "device": {
                    "serverId": "4f86de1d1212bac070000004",
                    "serverIdOld": 293,
                    "name": "mtx-ma4.wdc.sl",
                    "group": "MongoDB - Metrics Service",
                    "os": "linux"
                }
            },
        ]
    }
}
```

Pause
--
`POST /alerts/pause`

Pauses a specific alert.

*Only admin users can use this method*

**Parameters**

* `alertId` *string* - You can find this value by calling the `list` method or looking at the ID at the end of the URLs for editing an alert in the web interface.

**Request**

`https://api.serverdensity.com/1.4/alerts/pause?account=example.serverdensity.com`

**Response**

```json
{
    "status": 1,
    "data": {
        "paused": 1
    }
}
```

Resume
--
```POST /alerts/resume```

Resumes a specific alert.

*Only admin users can use this method*

**Parameters**

* `alertId` *string* - You can find this value by calling the `list` method or looking at the ID at the end of the URLs for editing an alert in the web interface.

**Request**

`https://api.serverdensity.com/1.4/alerts/resume?account=example.serverdensity.com`

**Response**

```json
{
    "status": 1,
    "data": {
        "resumed": 1
    }
}
```