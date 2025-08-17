---
weight: 300002
date: '2021-09-01T05:26:12.863Z'
draft: false
author: "Parash Maity"
title: "Number"
icon: "link"
toc: true
showTitle: false
description: "Fleare clients number functions"
publishdate: '2021-09-01T05:26:12.863Z'
tags: ["clients"]
---


#### Number functions


#### numSet

The numSet function stores a numeric value (integer or floating-point) in the key-value database. This command is designed to handle numerical data efficiently.

-> [Read More](/docs/cli-commands/number-commands/num-set)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
    const res = await client.numSet("user:1001:balance", 123);
    console.log(res);
```

Full Example

```ts
async function main() {
  const client = fleare.createClient("127.0.0.1", 9219);
  ...
  
  try {
    await client.connect();

    const res = await client.numSet("user:1001:balance", 12.55);
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
	res, err := client.NumSet("user:1001:balance", 123)
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}

	fmt.Println(res)
```

Full Example

```go
func main() {
	// Create a client with options
	client := fleare.CreateClient(&fleare.Options{
		Host:     "127.0.0.1",
		Port:     9219,
		PoolSize: 1,
	})

	err := client.Connect()
	if err != nil {
		fmt.Println(err)
		return
	}

	res, err := client.NumSet("user:1001:balance", 123)
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}
	fmt.Println(res)
}
```
Output

```text
""
```
---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### numGet

The numGet function retrieves a numerical value (integer or float) from the database associated with the given key. It only supports keys whose values are of type Number . If the key does not exist or the value is not a number, an appropriate error is returned.


-> [Read More](/docs/cli-commands/number-commands/num-get)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
const res = await client.numGet("user:1001:balance");
console.log(res);
```

Output

```text
12.55
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
	res, err := client.NumGet("user:1001:balance")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}

	fmt.Println(res)
```

Output

```text
12.55
```
---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### numIncr

The numIncr function increments a numeric value associated with a key. If the key does not exist, it sets the key to the given value (or to 1 by default). This command supports both integer and floating-point numbers.


-> [Read More](/docs/cli-commands/number-commands/num-incr)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
await client.numIncr("user:1001:balance", 10.05);
// get 
const res = await client.numGet("user:1001:balance");
console.log(res);
```

Output

```text
22.6
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
	res, err := client.NumIncr("user:1001:balance", 10.05)
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}

	fmt.Println(res)
```

Output

```text
133.05
```
---
{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### numDecr

The numDecr function decrements the numeric value stored at the specified key by a given amount. If the key does not exist, it initializes the key with the decremented value (i.e., 0 - value ). If no amount is provided, it decrements by 1 by default.


-> [Read More](/docs/cli-commands/number-commands/num-decr)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
await client.numDecr("user:1001:balance", 4);
// get 
const res = await client.numGet("user:1001:balance");
console.log(res);
```

Output

```text
18.6
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
	res, err := client.NumDecr("user:1001:balance", 5)
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}

	fmt.Println(res)
```

Output

```text
18.0
```
---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}
