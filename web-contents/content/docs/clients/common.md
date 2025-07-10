---
weight: 300001
date: '2021-09-01T05:26:12.863Z'
draft: false
author: "Parash Maity"
title: "Common usage"
icon: "link"
toc: true
showTitle: false
description: "Fleare clients common functions"
publishdate: '2021-09-01T05:26:12.863Z'
tags: ["clients"]
---


#### Common Client functions

This script demonstrates how to use the `fleare` client library to create a connection to a remote Fleare server instance, handle lifecycle events, and cleanly manage the connection lifecycle using an asynchronous pattern.


#### PING

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Import
```ts
import fleare from "fleare";
```

Simple use
```ts
    const res = await client.ping(["Test", 1, 2, 3]);
    console.log(res);
```

Full Example

```ts
async function main() {
  const client = fleare.createClient("127.0.0.1", 9219);
  ...
  
  try {
    await client.connect();

    const res = await client.ping(["Test", 1, 2, 3]);
    console.log(res);

  } catch (err) {
    console.error(err);
  } finally {
    await client.close();
  }
}
```
Output

```text
PONG Test 1 2 3

```


---

{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}


{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}


#### STATUS
The STATUS is used to retrieve the current state of the server, including server status, uptime, and detailed shard information. It helps users monitor the operational state of the server and its sharding configuration.

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
    const res = await client.status();
    console.log(res);
```

Output

```json
{
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


---

{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}


{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}