Alerts
===
* **Get history** - returns the full history for each time a specific alert has been triggered.
* `getLast` - returns the last 5 triggered alerts across the whole account.
* `getOpen` - returns the current open, non-fixed alerts.
* `getOpenNotified` - returns the current open, non-fixed alerts which have sent notifications.
* `list` - returns all configured alerts.
* `pause` - pauses a specific alert.
* `resume` - resumes a specific alert.

Get history
--
`GET /alerts/getHistory`

Returns the full history for each time a specific alert has been triggered.

**Parameters**

* `alertId` *string* - You can find this value by calling the `list` method or looking at the ID at the end of the URLs for editing an alert in the web interface.

**Request**

```GET http://api.serverdensity.com/VERSION/alerts/getHistory?account=example.serverdensity.com&alertId=4f86b63aff4bb6fc03000015```

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
``GET /alerts/getLast``

Returns the last 5 triggered alerts across the whole account.

**Request**

```GET http://api.serverdensity.com/1.4/alerts/getLast?account=example.serverdensity.com```

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