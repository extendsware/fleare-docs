---
weight: 300000
date: '2021-09-01T05:26:12.863Z'
draft: false
author: "Parash Maity"
title: "Connections"
icon: "link"
toc: true
showTitle: false
description: "Fleare clients connection documentations"
publishdate: '2021-09-01T05:26:12.863Z'
tags: ["clients"]
---


#### Fleare Client Connections

This script demonstrates how to use the `fleare` client library to create a connection to a remote Fleare server instance, handle lifecycle events, and cleanly manage the connection lifecycle using an asynchronous pattern.

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}


##### Import

```ts
import fleare from "fleare";
```

---

##### Usage Overview

```ts
async function main() {
  const client = fleare.createClient("127.0.0.1", 9219, {
    poolSize: 2,
    username: "root",
    password: "root",
    connectTimeout: 30000,
    maxRetries: 3,
    retryInterval: 10000
  });

  // Register lifecycle event listeners
  ...
  
  try {
    await client.connect();
  } catch (err) {
    console.error(err);
  } finally {
    await client.close();
  }
}
```

* Creates a Fleare client instance
* Subscribes to lifecycle events
* Initiates the connection
* Closes the client after execution

---

##### Client Configuration

```ts
const client = fleare.createClient("127.0.0.1", 9219, {
  poolSize: 2,
  username: "root",
  password: "root",
  connectTimeout: 30000,    // Max time to wait before failing a connection attempt (in ms)
  maxRetries: 3,            // Number of retry attempts if connection fails
  retryInterval: 10000      // Delay between retries (in ms)
});
```

This creates a new client with a connection pool size of 2, authentication credentials, and retry logic.

---

##### Client Events

| Event          | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| `connecting`   | Triggered before attempting to connect                       |
| `connected`    | Fired once the connection is successfully established        |
| `disconnected` | Emitted when the client disconnects from the server          |
| `error`        | Triggered on any connection or operational error             |
| `close`        | Fired when the connection is closed, gracefully or otherwise |
| `stateChanged` | Notifies state transitions like connecting → connected       |

Example:

```ts
client.on("connected", () => {
  console.log("Client connected successfully!");
});
```

---

##### Connection Lifecycle

```ts
await client.connect();
...
await client.close();
```

* `connect()` initiates the TCP connection to the Fleare server.
* `close()` gracefully shuts down the client connection.

---

##### Full Code Example

```ts
import fleare from "fleare";

async function main() {
  const client = fleare.createClient("127.0.0.1", 9219, {
    poolSize: 2,
    username: "root",
    password: "root",
    connectTimeout: 30000,
    maxRetries: 3,
    retryInterval: 10000
  });

  client.on("connecting", () => {
    console.log("Client is connecting...");
  });

  client.on("connected", () => {
    console.log("Client connected successfully!");
  });

  client.on("disconnected", () => {
    console.log("Client disconnected");
  });

  client.on("error", (err) => {
    console.error("Client error:", err.message);
  });

  client.on("close", () => {
    console.error("Client close:");
  });

  client.on("stateChanged", (state) => {
    console.log("Client state changed to:", state);
  });

  try {
    await client.connect();
  } catch (err) {
    console.error(err);
  } finally {
    await client.close();
  }
}

main();
```

---

{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}

##### Import
```go
import (
	"fmt"

	"github.com/extendsware/fleare-go"
)
```

##### Usage Overview
```go
client := fleare.CreateClient(&fleare.Options{
		Host: "127.0.0.1",
		Port: 9219,
		Username: "admin",
		Password: "password",
		PoolSize: 10,
	})
```

##### Connection Lifecycle

```ts
client.Connect();
...
client.Close();
```
##### Connection Events

```go
go monitorEvents(client)
```

```go
func monitorEvents(client *fleare.Client) {
	for event := range client.Events() {
		switch event.State {
		case fleare.StateConnecting:
			fmt.Println("Event is connecting...")
		case fleare.StateConnected:
			fmt.Println("Event connected successfully!")
		case fleare.StateDisconnecting:
			fmt.Println("Event Disconnecting")
		case fleare.StateDisconnected:
			fmt.Println("Event Disconnected")
		case fleare.StateError:
			fmt.Printf("Event error: %v", event.Error)
		}
	}
}
```


{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}
