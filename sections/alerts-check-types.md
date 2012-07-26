Alert Check Types
===
Check type for the `alerts/add` API method. These are values for the `checkType` parameter. See the [Alerts docs](alerts.md#add) for details.

**Plugins**

For plugins, you should specify the `checkType` parameter as the internal name which you find in the appropriate column from the Plugins tab in the web UI.

Apache
---
* `apacheReqPerSec` Apache requests per second
* `apacheBusyWorkers` Apache workers (busy)
* `apacheIdleWorkers` Apache workers (idle)

IIS
---
* `iisReqPerSec` IIS requests per second

HTTP (services/website monitoring)
---
* `httpStatusCode` HTTP - status code
* `httpResponseString` HTTP - response string found
* `httpResponseStringNotPresent` HTTP - response string not found
* `httpNotResponding` HTTP - not responding
* `httpResponseTime` HTTP - response time
* `httpResponseStringMD5` HTTP - response MD5 checksum

Misc
---
* `noData` No data received
* `processNotRunning` Process not running

MongoDB
---
* `mongoDBReplOptime` MongoDB replication - last optime
* `mongoDBReplCheck` MongoDB Replication - master failover/promotion


* `mongoDBCurrentConnections` MongoDB connections - current
* `mongoDBAvailableConnections` MongoDB connections - available


* `mongoDBTotalIndexSize` MongoDB total index size
* `mongoDBTotalDataSize` MongoDB total data size


* `mongoDBLockQueueReaders` MongoDB lock queue - readers
* `mongoDBLockQueueWriters` MongoDB lock queue - writers


* `mongoDBInsertOpCounters` MongoDB insert operations per second
* `mongoDBQueryOpCounters` MongoDB query operations per second
* `mongoDBUpdateOpCounters` MongoDB update operations per second
* `mongoDBDeleteOpCounters` MongoDB delete operations per second
* `mongoDBGetmoreOpCounters` MongoDB getmore operations per second
* `mongoDBCommandOpCounters` MongoDB command operations per second


* `mongoDBResidentMemory` MongoDB memory - resident
* `mongoDBVirtualMemory` MongoDB memory - virtual
* `mongoDBMappedMemory` MongoDB memory - mapped


* `mongoDBAccessesIndex` MongoDB index accesses per second
* `mongoDBHitsIndex` MongoDB index hits per second
* `mongoDBMissesIndex` MongoDB index misses per second
* `mongoDBMissRatioIndex` MongoDB index miss ratio per second


* `mongoDBRegularAsserts` MongoDB asserts - regular per second
* `mongoDBWarningAsserts` MongoDB asserts - warning per second
* `mongoDBMsgAsserts` MongoDB asserts - msg per second
* `mongoDBUserAsserts` MongoDB asserts - user per second
* `mongoDBRolloversAsserts` MongoDB asserts - rollovers per second

MySQL
---
* `mysqlConnections` MySQL connections per second
* `mysqlThreadsConnected` MySQL threads connected
* `mysqlSecondsBehindMaster` MySQL seconds behind master

nginx
---
* `nginxReqPerSec` Nginx requests per second
* `nginxConnections` Nginx connections

RabbitMQ
---
* `rabbitMQConnections` RabbitMQ connections (global, does not use the `queueName` parameter)
* `rabbitMQConsumers` RabbitMQ consumers
* `rabbitMQMessages` RabbitMQ messages
* `rabbitMQMessagesUnacknowledged` RabbitMQ messages - unacknowledged
* `rabbitMQMessagesUncommitted` RabbitMQ messages - uncommitted
* `rabbitMQQueueMemory` RabbitMQ memory - used

SQL Server
---
* `sqlServerLockRequestsPerSecond` SQL Server - lock requests/sec
* `sqlServerLockTimeoutsPerSecond` SQL Server - lock timeouts/sec
* `sqlServerNumberOfDeadlocksPerSecond` SQL Server - number of deadlocks/sec
* `sqlServerLockWaitsPerSecond` SQL Server - lock waits/sec
* `sqlServerLockWaitTime` SQL Server - lock wait time (ms)
* `sqlServerAverageWaitTime` SQL Server - average wait time (ms)
* `sqlServerDataFileSize` SQL Server - data file(s) size (KB)
* `sqlServerLogFileSize` SQL Server - log file(s) size (KB)
* `sqlServerLogFileUsedSize` SQL Server - log file(s) used size (KB)
* `sqlServerPercentLogUsed` SQL Server - percent log used
* `sqlServerActiveTransactions` SQL Server - active transactions
* `sqlServerTransactionsPerSecond` SQL Server - transactions/sec
* `sqlServerErrorsPerSecond` SQL Server - errors/sec
* `sqlServerActiveCursors` SQL Server - active cursors
* `sqlServerCursorMemoryUsage` SQL Server - cursor memory usage

System
---
* `loadAvrg` Load average


* `diskUsagePercent` % disk usage


* `ioStatsReadRequestsMerged` I/O - read requests merged per second
* `ioStatsWriteRequestsMerged` I/O - write requests merged per second
* `ioStatsReadRequests` I/O - read requests per second
* `ioStatsWriteRequests` I/O - write requests per second
* `ioStatsReadSize` I/O - KB per second read
* `ioStatsWriteSize` I/O - KB per second written
* `ioStatsAverageSize` I/O - average request sector size
* `ioStatsAverageQueueLength` I/O - average request queue length
* `ioStatsAverageTime` I/O - average request time (ms)
* `ioStatsAverageServiceTime` I/O - average service time (ms)
* `ioStatsPercentUtil` I/O - percentage of CPU time


* `cpuStatsUserLevel` CPU - user level
* `cpuStatsNice` CPU - user level nice priority
* `cpuStatsSys` CPU - system level
* `cpuStatsIOWait` CPU - I/O level
* `cpuStatsIRQ` CPU - interrupts
* `cpuStatsSoft` CPU - softirqs
* `cpuStatsSteal` CPU - steal
* `cpuStatsGuest` CPU - guest
* `cpuStatsIdle` CPU - idle


* `memPhysUsed` Memory - physical - used
* `memPhysFree` Memory - physical - free
* `memCached` Memory - physical - cached
* `memSwapUsed` Memory - swap - used
* `memSwapFree` Memory - swap - free


* `processCount` Process count