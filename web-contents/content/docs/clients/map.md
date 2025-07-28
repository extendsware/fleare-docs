---
weight: 300002
date: '2021-09-01T05:26:12.863Z'
draft: false
author: "Parash Maity"
title: "Map"
icon: "link"
toc: true
showTitle: false
description: "Fleare clients Map functions"
publishdate: '2021-09-01T05:26:12.863Z'
tags: ["clients"]
---


#### Map functions


#### mapSet

The mapSet function allows you to store or update a key-value pair within a map-type data structure under a specified top-level key. If the map does not already exist, it will be created automatically. This enables structured data to be efficiently grouped and manipulated under a single key.

-> [Read More](/docs/cli-commands/map-commands/map-set)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}


Example:
```ts
    const res = await client.mapSet("user-001:devices", "device-6d6f6sa66d", {
      "deviceName": "Pixel 7 Pro",
      "osVersion": "Android 14",
      "batteryLevel": "85%"
    });
    console.log(res);
```

Full Example

```ts
async function main() {
  const client = fleare.createClient("127.0.0.1", 9219);
  ...
  
  try {
    await client.connect();

    const res = await client.mapSet("user-001:devices", "device-6d6f6sa66d", {
      "deviceName": "Pixel 7 Pro",
      "osVersion": "Android 14",
      "batteryLevel": "85%"
    });
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


{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### mapCSet

The mapCSet function is used to create or overwrite a map at a specified key with a single key-value entry. If the key already exists, the previous map is completely replaced with the new one containing just the given mapKey and value .


-> [Read More](/docs/cli-commands/map-commands/map-cset)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Example:
```ts
const res = await client.mapCSet("user-001:devices", "device-6d6f6sa66d", {
  "deviceName": "Pixel 7 Pro",
  "osVersion": "Android 14",
  "batteryLevel": "85%"
});
console.log(res);
```

Output:

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


{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### mapDel

The mapDel function is used to delete either an entire map stored at a specific key or a specific field within that map. It supports both single-key and key-field deletion operations, ensuring efficient and flexible map data handling in memory.


-> [Read More](/docs/cli-commands/map-commands/map-del)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Example:
```ts
const res = await client.mapDel("user-001:devices", "device-6d6f6sa66d");
console.log(res);
```

Output:

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


{{% /tab %}}
{{% tab tabName="C#" %}}


{{% /tab %}}

{{< /tabs >}}

#### mapGet

The mapGet function allows users to retrieve values from a stored map object in the database. The user can either fetch the entire map stored at a given key or a specific field value inside the map using an optional mapKey .


-> [Read More](/docs/cli-commands/map-commands/map-get)

---

{{< tabs tabTotal="5">}}
{{% tab tabName="Node" %}}

Example:
```ts
const res = await client.mapGet("user-001:devices");
console.log(res);
```

Output:

```json
{
  "device-663abc5352": {
    "batteryLevel": "75%",
    "deviceName": "iPhone 14 Pro",
    "osVersion": "iOS 16"
  },
  "device-6d6f6sa66d": {
    "batteryLevel": "85%",
    "deviceName": "Pixel 7 Pro",
    "osVersion": "Android 14"
  }
}
```

Example with mapKye
```ts
const res = await client.mapGet("user-001:devices", "device-6d6f6sa66d");
console.log(res);
```

Output:

```json
{
  "batteryLevel": "85%",
  "deviceName": "Pixel 7 Pro",
  "osVersion": "Android 14"
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
