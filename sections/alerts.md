Alerts
===
* [Get history](#get-history) - returns the full history for each time a specific alert has been triggered.
* [Get last](#get-last) - returns the last 5 triggered alerts across the whole account.
* [Get open](#get-open) - returns the current open, non-fixed alerts.
* [Get open notified](#get-open-notified)` - returns the current open, non-fixed alerts which have sent notifications.
* [List](#list) - returns all configured alerts.
* [Pause](#pause) - pauses a specific alert.
* [Resume](#resume) - resumes a specific alert.

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