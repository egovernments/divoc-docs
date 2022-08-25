---
description: Redis service
---

# Troubleshooting

## Checking Status and Restarting Redis

To check the status of the Redis server:

* For getting into the Redis container, use the command “redis-cli”.
* Inside Redis, use the command “PING” -

&#x20;               \- If the response is “PONG” then the server is running.&#x20;

&#x20;               \- If the response is blank or anything else other than “PONG,” the server is not running.

* To get out of the Redis container: “exit”.

## **Process to restart the service if the Redis server is down**

Restarting service mainly involves killing the service and starting it again.

**Procedure to kill a service:**

* For killing any service on a Linux machine, we need the process\_id of the service. The process\_id which we get as the output number for further steps in killing the service by running the command is: **$ ps aux|grep redis**.
* For killing an unresponsive service on a Linux machine, replace the **process\_id\_of\_service** with the value that you have noted down in the above step:&#x20;

&#x20;      **$ sudo kill -9 process\_id\_of\_service**.

* To confirm if the service is killed: **$ sudo service redis-server status**.

**Procedure to start a service:**

* After successfully killing the service**,** to start the service: **$ sudo service redis-server start**.
* To check the status of the service: **$ sudo service redis-server status**.

Note: Check the status of the redis-server as mentioned above.



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
