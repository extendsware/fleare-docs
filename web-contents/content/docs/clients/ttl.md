---
weight: 300002
date: '2021-09-01T05:26:12.863Z'
draft: false
author: "Parash Maity"
title: "Time To Live (TTL)"
icon: "link"
toc: true
showTitle: false
description: "Fleare clients TTL functions"
publishdate: '2021-09-01T05:26:12.863Z'
tags: ["clients"]
---


#### TTL functions


#### ttlExpire

The ttlExpire function is used to set a Time-To-Live (TTL) on a key. Once the specified duration elapses, the key is automatically deleted from the database. This feature is helpful for scenarios involving temporary data, session expiration, or auto-cleanup mechanisms.

-> [Read More](/docs/cli-commands/ttl-commands/ttl-expire)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

* Default (Seconds)

* Seconds ( s )

* Minutes ( m )

* Hours ( h )

* Days ( d )

Simple use
```ts
    const res = await client.ttlExpire("user:greeting", 20);
    console.log(res);
```

Full Example

```ts
async function main() {
  const client = fleare.createClient("127.0.0.1", 9219);
  ...
  
  try {
    await client.connect();

    const res = await client.ttlExpire("user:greeting", "20m");
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
1
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

#### ttl

The ttl function checks the remaining time-to-live (in seconds) for a specific key in the database. It’s useful for understanding when a key is going to expire or confirming whether it has an expiration at all.


-> [Read More](/docs/cli-commands/ttl-commands/ttl)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Simple use
```ts
const res = await client.ttl("user:greeting");
console.log(res);
```

Output

```text
16
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
