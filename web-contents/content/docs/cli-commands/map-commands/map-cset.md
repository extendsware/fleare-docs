---
draft: false
title: MAP.CSET
is_title_visible: false
description: >-
  The MAP.CSET command is used to create or overwrite a map at a specified key
  with a single key-value entry.
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline

date: '2025-06-24T15:30:29.704Z'
authors: "Parash Maity"
is_breadcrumb_visible: true
is_menu_transparent: false
is_menu_visible: true
is_navigation_button_visible: false
is_table_of_content_visible: true
is_left_navigation_visible: true
is_root_content_hidden: false
padding: 15px 0
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-24T16:03:25.887Z'
is_summary_visible: true
is_taxonomy_visible: true
is_folder_visible_in_listing: false
weight: 2000000
id: /documentations/cli-commands/map-commands/map-cset.md
---
#### Command: `MAP.CSET` 

***

#### Overview

The `MAP.CSET` command is used to create or overwrite a map at a specified key with a single key-value entry. If the key already exists, the previous map is completely replaced with the new one containing just the given `mapKey` and `value` .

This command is useful in situations where you want to ensure that a key holds a map with only one specific entry, replacing any old map that was present under that key.

#### Command Name

**`MAP.CSET`**

#### Description

Sets or updates a key-value pair inside a map stored at the specified key.

⚠️ **Important**: This command **overwrites** any existing map at the specified key. The new map will contain **only** the provided `mapKey` and `value` .

***

#### Use Cases

* Replacing an existing device record with a new one.

* Initializing a key with a map containing a single entry.

* Resetting a user's map data with a new object.

#### Syntax

```bash 
MAP.CSET <key> <mapKey> <value>
```

*  `<key>` : The top-level key to store the map under.

*  `<mapKey>` : The key inside the map.

*  `<value>` : A valid JSON string representing the value for `mapKey` .

#### Permissions

* The user must have **write** permissions on the given key.

* No special roles required beyond standard modification rights.

***

#### Examples

##### Example 1: Add a new map with one entry

```bash 
localhost:9219> MAP.CSET user-001:devices device-6d6f6sa66d '{
  "deviceName": "Pixel 7 Pro",
  "osVersion": "Android 14",
  "batteryLevel": "85%"
}'
Ok

localhost:9219> MAP.GET user-001:devices
Ok {
  "deviceName": "Pixel 7 Pro",
  "osVersion": "Android 14",
  "batteryLevel": "85%"
}
```

##### Example 2: Overwrite map with a new entry

```bash 
localhost:9219> MAP.CSET user-001:devices device-663abc5352 '{
  "deviceName": "iPhone 14 Pro",
  "osVersion": "iOS 16",
  "batteryLevel": "75%"
}'

localhost:9219> MAP.GET user-001:devices
Ok {
  "deviceName": "iPhone 14 Pro",
  "osVersion": "iOS 16",
  "batteryLevel": "75%"
}
```

> Note: After the second call, the previous `"device-6d6f6sa66d"` entry is removed. Only the new entry remains.

***

#### Behavior on Error

| Error Condition                       | Message Example                                                   |
| ------------------------------------- | ----------------------------------------------------------------- |
| Missing arguments                     |  `ERR: InvalidArgsError: Key mapKey, and value must be provided`  |
| Invalid key format                    |  `ERR: InvalidKeyError: <details>`                                |
| Invalid mapKey (empty/invalid string) |  `ERR: InvalidMapKeyError: <details>`                             |
| Internal failure during map storage   |  `ERR: <internal error message>`                                  |

***

#### Internals (for developers)

* The old map stored at `<key>` is **deleted**.

* A new map object is created with `{<mapKey>: <value>}` 

***

 
