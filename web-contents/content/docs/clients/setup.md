---
weight: 205000
date: '2021-09-01T05:26:12.863Z'
draft: false
author: "Parash Maity"
title: "Setup"
icon: "link"
toc: true
showTitle: false
description: "Fleare clients installation and setup"
publishdate: '2021-09-01T05:26:12.863Z'
tags: ["clients"]
---


#### Installation and setup for clients


---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

#### Installation

```bash
npm install fleare
# or
yarn add fleare
````

---

#### Import Fleare


```ts
import fleare, { Options } from "fleare";
```

or
```js
const fleare = require("fleare-test").default;
```

#### Create a Client

```ts
const client = fleare.createClient("127.0.0.1", 9219, {
  poolSize: 10,
  username: "root",
  password: "root",
});
```

#### Connect to Fleare

```ts
client.connect().then(() => {
  console.log("✅ Connected to Fleare");
});
```

---

{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}

## Installation

```bash
go get github.com/extendsware/fleare-go
```

## Quick Start

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

	go monitorEvents(client)

	err := client.Connect()
	if err != nil {
		fmt.Println(err)
		return
	}

	// example of getting a value
	res, err := client.Get("key-1-1")

	if err != nil {
		fmt.Println(err)
		return
	}
	fmt.Println("Value for 'key':", res)

	defer client.Close()
}

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

