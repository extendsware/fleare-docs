---
weight: 300002
date: '2021-09-01T05:26:12.863Z'
draft: false
author: "Parash Maity"
title: "JSON Functions"
icon: "link"
toc: true
showTitle: false
description: "Fleare clients JSON functions"
publishdate: '2025-07-01T05:26:12.863Z'
tags: ["clients"]
---


#### JSON functions


#### jsonSet

The jsonSet function allows clients to store structured JSON objects under a specific key in a distributed, in-memory data store. If the key already exists, the stored JSON value is overwritten. This is particularly useful for schema-less data use cases like storing user profiles, configurations, and nested records.

-> [Read More](/docs/cli-commands/json-commands/json-set)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
    const res = await client.jsonSet("users:001", {"name":"John","age":30,"hobbies":["reading","hiking"]});
    console.log(res);
```

Full Example

```ts
async function main() {
  const client = fleare.createClient("127.0.0.1", 9219);
  ...
  
  try {
    await client.connect();

    const res = await client.jsonSet("users:001", {"name":"John","age":30,"hobbies":["reading","hiking"]});
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
res, err := client.JsonSet("user-001:devices", map[string]interface{}{"name": "John", "age": 30, "hobbies": []string{"reading", "hiking"}})
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

	res, err := client.JsonSet("user-001:devices", map[string]interface{}{"name": "John", "age": 30, "hobbies": []string{"reading", "hiking"}})
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

#### jsonAdd

The jsonAdd function allows users to insert or append a key-value pair into an existing JSON object stored at a given key. If the key does not exist, a new JSON object will be created. This command supports adding data at any depth using dot-notation paths.

* Description
Adds a key-value pair to a JSON object stored at the specified key in the database.

If the key doesn’t exist, a new JSON object will be initialized with the provided path and value.

Nested paths are supported using . (dot) notation. Intermediate objects will be created if they do not already exist.

The value must be a valid JSON string or primitive (string, number, boolean, array, etc.).

-> [Read More](/docs/cli-commands/json-commands/json-add)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Example:
```ts
await client.jsonSet("user:001", {"name":"John","age":30});
const res = await client.jsonAdd("user:001", "hobbies", ["reading","hiking"]);
console.log(res);
```

Output

```json
{ 
  "age": 30,
  "hobbies": [ "reading", "hiking" ], 
  "name": "John"
}

```


---

{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}

Set Data
```go
res, err := client.JsonSet("user-001:devices", map[string]interface{}{"name": "John", "age": 30})

```
Add Element
```go
	res, err := client.JsonAdd("user-001:devices", "hobbies", []string{"reading", "hiking"})
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}

	fmt.Println(res)
```
output
```json
{ 
  "age": 30,
  "hobbies": [ "reading", "hiking" ], 
  "name": "John" 
}
```
---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### jsonMerge

The jsonMerge function allows users to merge a new JSON object into an existing JSON object stored at a given key. This enables incremental updates to structured JSON data without overwriting the entire value.

-> [Read More](/docs/cli-commands/json-commands/json-merge)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Example:
```ts
await client.jsonSet("user:001", {"name":"John","age":30});
const res = await client.jsonMerge("user:001", {"age":40,"hobbies":["reading","hiking"]});
console.log(res);
```

Output

```json
{ 
  "age": 40,
  "hobbies": [ "reading", "hiking" ], 
  "name": "John" 
}

```
---

{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}


Example:
```go
	client.JsonSet("user:001", map[string]interface{}{"name": "John", "age": 30})

	res, err := client.JsonMerge("user:001", map[string]interface{}{"age": 40, "hobbies": []string{"reading", "hiking"}})
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}
```

Output

```json
{ 
  "age": 40,
  "hobbies": [ "reading", "hiking" ], 
  "name": "John" 
}

```
---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### jsonRemove

The jsonRemove function allows users to delete a specific field or the entire JSON object associated with a key stored in the Fleare in-memory database. It supports nested paths using dot notation and ensures safe deletion based on key validation and type checking.

-> [Read More](/docs/cli-commands/json-commands/json-remove)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Example:
```ts
await client.jsonSet("user:001", {"name":"Foo","active":true,"score":42});
const res = await client.jsonRemove("user:001", "active");
console.log(res);
```

Output

```json
{
  "name":"Foo",
  "score":42
}

```

---

{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}


Example:
```go
	client.JsonSet("user:001", map[string]interface{}{"name": "Foo", "active": true, "score": 42})

	res, err := client.JsonRemove("user:001", "active")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}

	fmt.Println(res)
```

Output

```json
{
  "name":"Foo",
  "score":42
}

```
---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### jsonSetRes

The jsonSetRes function stores a JSON object at a specified key in the database and simultaneously replaces specified fields with reference pointers to other keys. This allows relational-like linking between JSON documents using reference tags. This command is useful for creating relationships between JSON documents.

-> [Read More](/docs/cli-commands/json-commands/json-setref)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Example set:
```ts
await client.jsonSet("users:001", {"name":"John","age":30,"hobbies":["reading","hiking"]});
const res = await client.jsonGet("orders:OD001");
console.log(res);
```

Output
```json
{"name":"John","age":30,"hobbies":["reading","hiking"]}
```

Example setRef
```js
await client.jsonSetRef("orders:OD001", {"orderId":"orders:OD001","details":"This order is for a new laptop.","status":"pending"}, {"userId":"users:001"});
const res = await client.jsonGet("orders:OD001", "", "userId");
console.log(res);
```

Output

```json
{
  "_userId": { "age": 30, "hobbies": [ "reading", "hiking" ], "name": "John" },
  "details": "This order is for a new laptop.",
  "orderId": "orders:OD001",
  "status": "pending",
  "userId": "$ref:users:001"
}

```

---

{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}


Example set:
```go
	res, err := client.JsonSet("user:001", map[string]interface{}{"name": "Foo", "active": true, "score": 42})

	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}

	fmt.Println(res)
```

Example setRef
```go
res, err := client.JsonSetRef("orders:OD001",
		map[string]interface{}{"orderId": "orders:OD001", "details": "This order is for a new laptop.", "status": "pending"},
		map[string]interface{}{"userId": "user:001"})

if err != nil {
  fmt.Println("Error checking existence:", err)
  return
}
```

```go
	res, err := client.JsonGet("orders:OD001", "", "userId")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}
	fmt.Println(res)
```

Output

```json
{
  "_userId": {"name": "Foo", "active": true, "score": 42},
  "details": "This order is for a new laptop.",
  "orderId": "orders:OD001",
  "status": "pending",
  "userId": "$ref:users:001"
}

```

---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### jsonGet

The jsonGet function retrieves JSON data stored at a specified key. You can optionally query nested fields within the JSON object using a dot-path syntax. Additionally, the command supports resolving references (e.g., $ref: values) and attaching the referenced data inline in the response.


-> [Read More](/docs/cli-commands/json-commands/json-get)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Example set:
```ts
await client.jsonSet("users:001", {"name":"John","age":30,"hobbies":["reading","hiking"]});
const res = await client.jsonGet("orders:OD001");
console.log(res);
```

Output
```json
{"name":"John","age":30,"hobbies":["reading","hiking"]}
```

Example with path
```ts
const res = await client.jsonGet("orders:OD001", "hobbies");
console.log(res);
```

Output
```json
["reading","hiking"]
```

Example ref
```js
await client.jsonSetRef("orders:OD001", {"orderId":"orders:OD001","details":"This order is for a new laptop.","status":"pending"}, {"userId":"users:001"});
const res = await client.jsonGet("orders:OD001", "", "userId");
console.log(res);
```

Output

```json
{
  "_userId": { "age": 30, "hobbies": [ "reading", "hiking" ], "name": "John" },
  "details": "This order is for a new laptop.",
  "orderId": "orders:OD001",
  "status": "pending",
  "userId": "$ref:users:001"
}

```

---

{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}


Example set:
```go
client.JsonSet("user:001", map[string]interface{}{"name":"John","age":30,"hobbies":["reading","hiking"]})
res, err := client.JsonGet("orders:OD001")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}
	fmt.Println(res)
```

Output
```json
{"name":"John","age":30,"hobbies":["reading","hiking"]}
```

Example with path
```go
res, err := client.JsonGet("orders:OD001", "hobbies")
if err != nil {
  fmt.Println("Error checking existence:", err)
  return
}
fmt.Println(res)
```

Output
```json
["reading","hiking"]
```

Example `#ref:`
```go

	client.JsonSet("user:001", map[string]interface{}{"name": "Foo", "active": true, "score": 42})

	_, err = client.JsonSetRef("orders:OD001",
		map[string]interface{}{"orderId": "orders:OD001", "details": "This order is for a new laptop.", "status": "pending"},
		map[string]interface{}{"userId": "user:001"})
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}

	res, err := client.JsonGet("orders:OD001", "", "userId")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}
	fmt.Println(res)
```

Output

```json
{
  "_userId": { "age": 30, "hobbies": [ "reading", "hiking" ], "name": "John" },
  "details": "This order is for a new laptop.",
  "orderId": "orders:OD001",
  "status": "pending",
  "userId": "$ref:user:001"
}

```

---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}
