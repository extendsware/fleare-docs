---
weight: 300002
date: '2021-09-01T05:26:12.863Z'
draft: false
author: "Parash Maity"
title: "String"
icon: "link"
toc: true
showTitle: false
description: "Fleare clients string functions"
publishdate: '2021-09-01T05:26:12.863Z'
tags: ["clients"]
---


#### String functions


#### strSet

The strSet command stores or updates a string value associated with a specified key. If the key already exists, its value is overwritten.


-> [Read More](/docs/cli-commands/string-commands/str-set)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
    const res = await client.strSet("user:greeting", "World World")
    console.log(res);
```

Full Example

```ts
async function main() {
  const client = fleare.createClient("127.0.0.1", 9219);
  ...
  
  try {
    await client.connect();

    const res = await client.strSet("user:greeting", "World World")
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
res, err := client.StrSet("user:123", "Hello, Welcome to our service! Regards, Team Fleare")
if err != nil {
  fmt.Println("Error checking existence:", err)
  return
}
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

	res, err := client.StrSet("user:123", "Hello, Welcome to our service! Regards, Team Fleare")
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

#### strAppend

The strAppend command is used to append one or more string values to an existing string stored at a given key. If the key does not exist, it creates a new entry with the concatenated value.

-> [Read More](/docs/cli-commands/string-commands/str-append)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
    const res = await client.strAppend("user:greeting", "World", " World")
    console.log(res);
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
res, err := client.StrAppend("greeting", "Hello", " World")
if err != nil {
  fmt.Println("Error checking existence:", err)
  return
}

fmt.Println(res)
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

#### strRange

The strRange command returns a substring from a string value stored at a specified key, based on start and end offsets (inclusive). It supports negative indices, enabling easy access to characters counted from the end of the string.

-> [Read More](/docs/cli-commands/string-commands/str-range)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
    const res = await client.strRange("user:greeting", 0, -1);
    console.log(res);
```

Output

```text
World World
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
	res, err := client.StrRange("greeting", 0, -1)
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}

	fmt.Println(res)
```

Output

```text
World World
```
---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### strGet

The strGet command is used to retrieve the string value associated with a specified key. If the key does not exist or has a different data type, appropriate responses are returned. This command is safe to use for read-only operations and ensures type safety for string keys.

-> [Read More](/docs/cli-commands/string-commands/str-get)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
const res = await client.strGet("user:greeting");
console.log(res);
```

Output

```text
World World
```


{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}

Simple use
```go
	res, err := client.StrGet("greeting")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}

	fmt.Println(res)
```

Output

```text
World World
```
---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}


#### strLength

The strLength command is used to retrieve the length (in characters) of a string value stored at a specified key in the Fleare key-value store. If the key does not exist, it returns 0. It validates the key and ensures the value is of string type.

-> [Read More](/docs/cli-commands/string-commands/str-length)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
const res = await client.strLength("user:greeting");
console.log(res);
```

Output

```text
11
```


{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}

Simple use
```go
	res, err := client.StrLength("greeting")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}

	fmt.Println(res)
```

Output

```text
11
```
---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

