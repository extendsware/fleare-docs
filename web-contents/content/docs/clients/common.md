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

Sends a PING command to the server and receives a PONG response. Optionally, arguments can be passed which are echoed back after PONG .
This is commonly used to check if the server is responsive (like a health check or heartbeat).


-> [Read More](/docs/cli-commands/ping)

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

Import
```go
import (
	"github.com/extendsware/fleare-go"
)
```

Simple use
```ts
    res, err := await client.Ping(["Test", 1, 2, 3]);
    fmt.Println(res)
```

Full Example

```go
package main

import (
	"fmt"

	"github.com/extendsware/fleare-go"
)

func main() {
	// Create client
	client := fleare.CreateClient(&fleare.Options{
		Host: "127.0.0.1",
		Port: 9219,
		Username: "admin",
		Password: "password",
		PoolSize: 10,
	})

	err := client.Connect()
	if err != nil {
		fmt.Println(err)
		return
	}

	defer client.Close()
	// example of getting a value
	res, err := client.Ping("Test", "1", "2", "3")

	if err != nil {
		fmt.Println(err)
		return
	}
	fmt.Println("Value for 'PING':", res)
}
```
Output

```text
Value for 'PING': PONG Test 1 2 3

```

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}


#### STATUS
The STATUS is used to retrieve the current state of the server, including server status, uptime, and detailed shard information. It helps users monitor the operational state of the server and its sharding configuration.

-> [Read More](/docs/cli-commands/status)

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

```go
	res, err := client.Status()

	if err != nil {
		fmt.Println(err)
		return
	}

	// parse the res as json
	jsonBytes, err := json.MarshalIndent(res, "", "  ")
	if err != nil {
		fmt.Println("Error marshaling to JSON:", err)
		return
	}
	fmt.Println(string(jsonBytes))
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

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### EXISTS
The EXISTS command is used to verify the existence of one or more keys in the database. It returns the count of keys that exist from the list provided.

-> [Read More](/docs/cli-commands/exists)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
    const res = await client.exists("key1");
    console.log(res);
```

Output

```json
1
```
multi key use
```ts
    const res = await client.exists("key1", "key2", "no-key");
    console.log(res);
```

Output

```json
2
```


---

{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}

```go
res, err := client.Exists("key1", "key2")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}

	fmt.Println(res)
```

Output
```text
2
```
---
{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### SESSION
The SESSION command returns the current session information for the authenticated client. It is typically used for diagnostics, auditing, or session lifecycle inspection.

-> [Read More](/docs/cli-commands/session)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
    const res = await client.session()
    console.log(res);
```

Output

```json
{
  "created_at": "2025-05-01T17:33:15.497273Z",
  "last_accessed_at": "2025-05-01T17:33:15.497273Z",
  "session_id": "8-127.0.0.1:53531",
  "status": 1,
  "user": {
    "Password": "*******",
    "Role": "Admin",
    "Username": "admin"
  }
}
```
---

{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}


Simple use
```go
  res, err := client.Session()
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}
	// parse the res as json
	jsonBytes, err := json.MarshalIndent(res, "", "  ")
	if err != nil {
		fmt.Println("Error marshaling to JSON:", err)
		return
	}
	fmt.Println(string(jsonBytes))
```

Output

```json
{
  "created_at": "2025-05-01T17:33:15.497273Z",
  "last_accessed_at": "2025-05-01T17:33:15.497273Z",
  "session_id": "8-127.0.0.1:53531",
  "status": 1,
  "user": {
    "Password": "*******",
    "Role": "Admin",
    "Username": "admin"
  }
}
```
---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### SET
The SET command is used to store a key-value pair in the database. If the key already exists, the value is overwritten. It is a common operation to persist data in memory Database.

-> [Read More](/docs/cli-commands/set)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}


Simple use
```ts
const res = await client.set("greetings", "Hello, Welcome to our service! Regards, Team")
```

Json use 
```ts
const res = await client.set("user:123", {
    "id":123,
    "name":"Alice",
    "roles":[
        "admin",
        "editor"
    ]
})
console.log(res);
```

Output empty body

```json
""
```


---

{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}


Simple use
```go
res, err := client.Set("greetings", "Hello, Welcome to our service! Regards, Team Fleare")
```

Json use 
```go
	res, err := client.Set("user:123", map[string]interface{}{
		"id":   123,
		"name": "Alice",
		"roles": []string{
			"admin",
			"editor",
		},
	})
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}

	fmt.Println(res)
```

Output empty body

```json
""
```


{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}


#### GET
The GET command retrieves the value associated with a given key from the in-memory database. If the value is a nested JSON object, an optional path can be provided to extract specific nested fields.

-> [Read More](/docs/cli-commands/get)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}


Simple use
```ts
const res = await client.get("user:123");
console.log(res);
```

Output body

```json
{
    "id":123,
    "name":"Alice",
    "roles":[
        "admin",
        "editor"
    ]
}
```

Using path
```ts
const res = await client.get("user:123", "roles")
console.log(res);
```

Output body

```json
[ "admin", "editor" ]
```


---

{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}

```go

	res, err := client.Get("user:123")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}

	// parse the res as json
	jsonBytes, err := json.MarshalIndent(res, "", "  ")
	if err != nil {
		fmt.Println("Error marshaling to JSON:", err)
		return
	}
	fmt.Println(string(jsonBytes))

```
Output

```json
{
  "id": 123,
  "name": "Alice",
  "roles": [
    "admin",
    "editor"
  ]
}
```

Using Path
```go
	res, err := client.Get("user:123", "roles")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}

	// parse the res as json
	jsonBytes, err := json.MarshalIndent(res, "", "  ")
	if err != nil {
		fmt.Println("Error marshaling to JSON:", err)
		return
	}
	fmt.Println(string(jsonBytes))
```

Output

```json
[ "admin", "editor" ]

```

---
{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### DELETE
The DELETE command is used to remove a key-value pair from the in-memory database. It ensures the specified key is validated, removes it from the appropriate memory shard.

-> [Read More](/docs/cli-commands/delete)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}


Simple use
```ts
const res = await client.del("user:123");
console.log(res);
```

Output empty body

```json
""
```

---

{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}

```go
	res, err := client.Del("user:123")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}
  ```

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}