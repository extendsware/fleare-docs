---
weight: 300003
date: '2021-09-01T05:26:12.863Z'
draft: false
author: "Parash Maity"
title: "Array and List"
icon: "link"
toc: true
showTitle: false
description: "Fleare clients List functions"
publishdate: '2021-09-01T05:26:12.863Z'
tags: ["clients"]
---


#### Array and List functions


#### listSet

The listSet function clears the existing elements associated with a given list key and sets the provided values as the new list elements. It effectively replaces any previously stored data under the key with the new list.

-> [Read More](/docs/cli-commands/list-commands/list-set)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
    const res = await client.listSet("myList", "First element");
    console.log(res);
```
Set Multiple items
```ts
    const res = await client.listSet("myList", "First", "Second", "Third");
    console.log(res);
```

Full Example

```ts
async function main() {
  const client = fleare.createClient("127.0.0.1", 9219);
  ...
  
  try {
    await client.connect();

    const res = await client.listSet("myList", "First", "Second", "Third");
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
3
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
  res, err := client.ListSet("myList", "First")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}
	fmt.Println(res)
```
Set Multiple items

```go
  res, err := client.ListSet("myList", "First", "Second", "Third")
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

	res, err := client.ListSet("myList", "First", "Second", "Third")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}
	fmt.Println(res)
}
```
Output

```text
3
```
---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### listIset

The listIset function allows users to insert or replace an element at a specified index in a list stored at the provided key. This operation is index-based, and it does not extend the list—an out-of-range index returns an error.


-> [Read More](/docs/cli-commands/list-commands/list-iset)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
const res = await client.listIset("myKey", 0, "This is my first element");
console.log(res);
```

Get item
```ts
const res = await client.get("myKey", 0);
console.log(res);
```

Output

```text
"This is my first element"
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
	res, err := client.ListISet("myList", 2, "This is my first element")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}
	fmt.Println(res)
```

Get item
```go
res1, err := client.ListGet("myList", 2)
	fmt.Println(res1)
```

Output

```text
"This is my first element"
```
---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### listPush

The listPush function inserts one or more elements at the beginning of a list associated with a specific key in the Fleare in-memory database. If the key does not exist, a new list is created. If the key exists but holds a non-list data type, an error is returned.


-> [Read More](/docs/cli-commands/list-commands/list-push)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
const res = await client.listPush("myList", "First");
```
Multiple items
```ts
const res = await client.listPush("myList", "Second", "Third");
```

Get item
```ts
const res = await client.get("myList");
console.log(res);
```

Output

```json
["First" "Second" "Third"]
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
	res, err := client.ListPush("myList", "First")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}
	fmt.Println(res)
```
Multiple items
```ts
	res, err := client.ListPush("myList", "First", "Second", "Third" )
```

Get item
```go
res, err := client.ListGet("myList")
fmt.Println(res)
```

Output

```json
["First" "Second" "Third"]
```

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}


#### listPop

The listPop function return (pops) a single element from the beginning (index 0) of a list stored at a specified key. If the list becomes empty after the pop, the key is removed from the store.


-> [Read More](/docs/cli-commands/list-commands/list-pop)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
const res = await client.listPop("myKey");
console.log(res);
```

Output

```text
"This is my first element"
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
	res, err := client.ListPop("myList")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}
	fmt.Println(res)
```

Output

```text
"This is my first element"
```
---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### listGet

The listGet function retrieves one or more elements from a list stored at a specific key. If an index is provided, it returns the value at that index; otherwise, it returns the entire list.


-> [Read More](/docs/cli-commands/list-commands/list-get)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
const res = await client.listGet("myKey");
console.log(res);
```

Output

```json
["This is my first element"]
```

Using index
```ts
const res = await client.listGet("myKey", 0);
console.log(res);
```

Output

```json
"This is my first element"
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
	res, err := client.ListGet("myList")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}
	fmt.Println(res)
```

Output

```json
["This is my first element"]
```

Using index
```go
	res, err := client.ListGet("myList", 0)
	fmt.Println(res)
```

Output

```json
"This is my first element"
```
---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### listLen

The listLen function is used to retrieve the number of elements in a list stored at a given key. It validates the key, checks for the appropriate data type, and returns the size of the list. If the key is not associated with a list, or if the key doesn’t exist, a relevant error or response is returned.


-> [Read More](/docs/cli-commands/list-commands/list-len)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
const res = await client.listLen("myKey");
console.log(res);
```

Output

```json
3
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
	res, err := client.ListLen("myList")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}
	fmt.Println(res)
```

Output

```json
3
```

---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### listFind

The listFind function filters elements from a list stored at a specified key using various comparison operators and path-based expressions. It supports FIND primitives (strings, numbers, booleans) and objects (using nested field paths).


-> [Read More](/docs/cli-commands/list-commands/list-find)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Push items
```ts
const res = await client.listPush("myList", 10, 20, 30, 40, 50, 60, 70, 80, 90, 100);
```

Simple use
```ts
const res = await client.listFind("myList", ":30");
console.log(res);
```

Output

```json
[30]
```

Simple use 2
```ts
const res = await client.listFind("myList", ">30");
console.log(res);
```

Output

```json
[40, 50, 60, 70, 80, 90, 100]
```

---

{{% /tab %}}
{{% tab tabName="Java" %}}


{{% /tab %}}
{{% tab tabName="Python" %}}


{{% /tab %}}
{{% tab tabName="GoLang" %}}


Set items
```go
client.ListSet("myList", 10, 20, 30, 40, 50, 60, 70, 80, 90, 100)
```

Simple use
```go
res, err := client.ListFind("myList", ":30")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}
	fmt.Println(res)
```

Output

```json
[30]
```

Simple use 2
```ts
res, err := client.ListFind("myList", ">30")
	if err != nil {
		fmt.Println("Error checking existence:", err)
		return
	}
	fmt.Println(res)
```

Output

```json
[40, 50, 60, 70, 80, 90, 100]
```

---

{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}
