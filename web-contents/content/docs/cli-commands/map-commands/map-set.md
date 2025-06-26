---
draft: false
title: MAP.SET
is_title_visible: false
description: >-
  The MAP.SET command allows you to store or update a key-value pair within a
  map-type data structure under a specified top-level key.
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline

date: '2025-06-24T15:23:41.976Z'
authors: "Parash Maity"
is_breadcrumb_visible: true
is_menu_transparent: false
is_menu_visible: true
is_navigation_button_visible: false
is_table_of_content_visible: true
is_left_navigation_visible: true
is_root_content_hidden: false
padding: 15px 0
is_summary_visible: true
is_taxonomy_visible: true
is_folder_visible_in_listing: false
id: /documentations/cli-commands/map-commands/map-set.md
weight: 1000000
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-24T16:03:25.885Z'
---
#### **Command**: `MAP.SET` 

***

#### **Overview**

The `MAP.SET` command allows you to store or update a key-value pair within a map-type data structure under a specified top-level key. If the map does not already exist, it will be created automatically. This enables structured data to be efficiently grouped and manipulated under a single key.

#### **Command Name**

 `MAP.SET` 

#### **Description**

 `MAP.SET <key> <mapKey> <value>` 

This command sets or updates the value of `<mapKey>` within the map stored at `<key>` .

* If `<key>` does not exist, a new map is created.

* If `<key>` exists and holds a map, the `<mapKey>` is inserted or updated.

* The `<value>` must be a valid JSON string representing a primitive or object.

#### **Use Cases**

* **Device tracking** per user where each device is uniquely keyed.

* **Configuration storage** with nested property overrides.

* **Session metadata** per client or session ID.

* **Caching structured objects** grouped under a parent key.

***

#### **Syntax**

```bash 
MAP.SET <key> <mapKey> <value>
```

*  `<key>` : Parent map key (e.g., `user-001:devices` )

*  `<mapKey>` : Sub-key inside the map (e.g., `device-6d6f6sa66d` )

*  `<value>` : JSON string representing the value (e.g., `'{"osVersion":"Android 14"}'` )

#### **Permissions**

* **Write access** to the target shard associated with the key is required.

* Command will fail if write operations are disabled due to system policies or mode.

***

#### **Examples**

##### Set map entries for user devices:

```bash 
localhost:9219> MAP.SET user-001:devices device-6d6f6sa66d '{
  "deviceName": "Pixel 7 Pro",
  "osVersion": "Android 14",
  "batteryLevel": "85%"
}'
Ok

localhost:9219> MAP.SET user-001:devices device-663abc5352 '{
  "deviceName": "iPhone 14 Pro",
  "osVersion": "iOS 16",
  "batteryLevel": "85%"
}'
Ok
```

##### Retrieve full map:

```bash 
localhost:9219> MAP.GET user-001:devices
Ok {
  device-6d6f6sa66d: {
    deviceName: "Pixel 7 Pro",
    osVersion: "Android 14",
    batteryLevel: "85%"
  },
  device-663abc5352: {
    deviceName: "iPhone 14 Pro",
    osVersion: "iOS 16",
    batteryLevel: "85%"
  }
}
```

##### Retrieve specific entry:

```bash 
localhost:9219> MAP.GET user-001:devices device-663abc5352
Ok {
  deviceName: "iPhone 14 Pro",
  osVersion: "iOS 16",
  batteryLevel: "85%"
}
```

***

#### **Behavior on Error**

| Scenario                      | Error Message                                                                                        |
| ----------------------------- | ---------------------------------------------------------------------------------------------------- |
| Missing arguments             |  `InvalidArgsError: Key mapKey, and value must be provided, Syntax: MAP.SET <key> <mapKey> <value>`  |
| Invalid map key               |  `InvalidMapKeyError: <details>`                                                                     |
| Value exists but is not a map |  `InvalidValueError: The current value associated with the provided key must be a Map type`          |

***

 
