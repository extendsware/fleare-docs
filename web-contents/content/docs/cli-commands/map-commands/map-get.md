---
draft: false
title: MAP.GET
is_title_visible: false
description: >-
  The MAP.GET command allows users to retrieve values from a stored map object
  in the database.
date: '2025-06-24T15:37:51.255Z'
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
id: /documentations/cli-commands/map-commands/map-get.md
weight: 3000000
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-24T16:03:25.886Z'
---
#### **Command**: `MAP.GET` 

***

#### **Overview**

The `MAP.GET` command allows users to retrieve values from a stored map object in the database. The user can either fetch the **entire map** stored at a given key or **a specific field value** inside the map using an optional `mapKey` .

#### **Command Name**

`MAP.GET`

#### **Description**

The command fetches structured JSON data stored as a map in the database. It can return:

* The **full map** (when only the key is provided)

* A **single value** from the map (when both key and mapKey are provided)

This is especially useful for structured entities like:

* User profiles

* Device settings

* Application configurations

* Metadata fields

#### **Use Cases**

| Scenario                   | Description                                                               |
| -------------------------- | ------------------------------------------------------------------------- |
| View all devices of a user | Retrieve a list of all registered devices for a user using their user key |
| Get config detail          | Fetch only a specific field (like `batteryLevel` ) from a nested map      |
| Debug map contents         | Quickly inspect what values are stored under a given key                  |

***

#### **Syntax**

```bash 
MAP.GET <key> [<mapKey>]
```

#### Arguments

| Argument     | Required | Description                                                              |
| ------------ | -------- | ------------------------------------------------------------------------ |
|  `<key>`     | Yes      | The top-level key identifying the stored map                             |
|  `[mapKey]`  | No       | A specific key within the stored map to retrieve its corresponding value |

***

#### **Permissions**

* Requires **read** access to the provided key.

* No special privileges required beyond standard user-level access.

***

#### **Examples**

#### Example 1: Retrieve full map

**Input:**

```
localhost:9219> MAP.GET user-001:devices
```

**Output:**

```bash 
Ok {
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

***

##### Example 2: Retrieve value by map key

**Input:**

```
localhost:9219> MAP.GET user-001:devices device-663abc5352
```

**Output:**

```bash 
Ok {
  "batteryLevel": "75%",
  "deviceName": "iPhone 14 Pro",
  "osVersion": "iOS 16"
}
```

***

##### Example 3: Retrieve a non-existent map key

**Input:**

```
localhost:9219> MAP.GET user-001:devices device-nonexistent
```

**Output:**

```
Ok ""
```

***

#### **Behavior on Error**

| Error Case              | Message                                                                                    |
| ----------------------- | ------------------------------------------------------------------------------------------ |
| Too many arguments (>2) |  `InvalidArgsError: More than 2 args not supported, Supported args Key or key and mapKey`  |

***

#### **Notes**

* The command does **not** return an error if the `mapKey` is not found. It returns an **empty string** ( `""` ).

 
