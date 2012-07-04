Alerts
===
* `getHistory` - returns the full history for each time a specific alert has been triggered.
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
{"status":1,"data":{"alerts":[{"alert":{"alertId":{"$id":"4f86b63aff4bb6fc03000015"},"timeAlertedGMT":"2012-06-08T10:37:16+00:00","alertTriggeredId":{"$id":"4fd1d5dcd21be404a63395ac"},"fixed":1,"timeAlerted":"2012-06-08 10:37:16","timeAlertedText":"Jun 8th","timeFixedGMT":"2012-06-08T10:40:10+00:00","checkType":"noData","triggeredValue":"6 mins","notificationType":["email"],"lastNotified":"2012-06-08 10:37:16","timestamp":null,"timeFixed":"2012-06-08 10:40:10","checkTypeText":"No data received","notificationTypeText":"E-mail"},"users":[],"usersText":"PagerDuty Critical","device":{"serverId":291,"name":"a1.wdc.sl","cloudMonitoring":false}}]}}```