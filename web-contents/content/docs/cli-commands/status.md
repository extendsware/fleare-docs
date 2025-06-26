---
weight: 100
date: '2021-09-01T05:26:12.863Z'
draft: false
author: "Parash Maity"
title: "STATUS"
icon: "rocket_launch"
toc: true
showTitle: false
description: "The STATUS command is used to retrieve the current state of the server"
publishdate: '2021-09-01T05:26:12.863Z'
tags: ["STATUS"]
---

---
#### Comman: `STATUS`

---

#### Overview

The `STATUS` command is used to retrieve the current state of the server, including server status, uptime, and detailed shard information. It helps users monitor the operational state of the server and its sharding configuration.

***

#### Command Name

 `STATUS` 

***

#### Description

Retrieves the status of the server. The response includes:

* Server running status.

* Uptime since the last server start.

* Shard metadata such as ID, host address, key count, name, total memory used per shard, and total shard count.

***

#### Syntax

```text 
STATUS
```

***

#### Permissions

* No special permissions required.

* Accessible by any connected client.

***

#### Input Examples

**Example 1:**

```bash 
localhost:9219> status
```

***

#### Output Examples

**Example 1: Server running with two shards**

```json 
Ok {
  "server_status": "running",
  "shard_info": {
    "0": {
      "ID": "0",
      "host_address": "localhost:9291",
      "key_length": 123,
      "name": "Shard 0",
      "total_size": "8 bytes"
    },
    "1": {
      "ID": "1",
      "host_address": "localhost:9291",
      "key_length": 454,
      "name": "Shard 1",
      "total_size": "8 bytes"
    },
    "shard_count": 2
  },
  "up_time": "2025-06-18T11:30:45.123456789Z"
}
```

***

#### Behavior on Error

**Note:** Errors are returned in a standardized response format if encountered during execution.

***

#### Use Cases

* **Monitoring:** Used by administrators or monitoring tools to check if the server is up and running.

* **Diagnostics:** Helps in debugging by displaying which shards are active and their current load (via key count and size).

* **Health Checks:** Used in automated health checks and service dashboards to ensure sharding is functioning correctly.

 
