---
draft: false
title: MAP.DEL
is_title_visible: false
description: >-
  The MAP.DEL command is used to delete either an entire map stored at a
  specific key or a specific field within that map.

date: '2025-06-24T15:43:21.413Z'
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
  last_published: '2025-06-24T16:03:25.888Z'
is_summary_visible: true
is_taxonomy_visible: true
is_folder_visible_in_listing: false
weight: 4000000
id: /documentations/cli-commands/map-commands/map-del.md
---
#### Command: `MAP.DEL` 

***

#### Overview

The `MAP.DEL` command is used to delete either an entire map stored at a specific key or a specific field within that map. It supports both single-key and key-field deletion operations, ensuring efficient and flexible map data handling in memory.

#### Command Name

 `MAP.DEL` 

#### Description

 `MAP.DEL` deletes a map object entirely or removes a specific key-value pair (field) from the map stored at a given key.

* If only `<key>` is provided, the entire map object will be removed.

* If both `<key>` and `<mapKey>` are provided, only the field `<mapKey>` is deleted from the map.

#### Use Cases

* Remove a user's entire settings map.

* Delete a device entry from a user's device map.

* Clean up stale or invalid configuration fields without affecting the rest of the map.

* Implement dynamic field pruning for memory optimization.

***

#### Syntax

```bash 
MAP.DEL <key> [<mapKey>]
```

*  `<key>` : The main key pointing to the map (required).

*  `<mapKey>` : The specific field in the map to delete (optional).

#### Permissions

* Write access to the key's shard.

* Authorization to modify or delete in-memory objects.

***

#### Examples

##### 1. **Delete a specific field from a map**

Assume the current value of `user-001:devices` is:

```bash 
{
  "device-6d6f6sa66d": "Android",
  "device-x4d5f2c1b2e": "iOS"
}
```

```bash 
localhost:9219> MAP.DEL user-001:devices device-6d6f6sa66d
Ok
```

Result:

```bash 
{
  "device-x4d5f2c1b2e": "iOS"
}
```

***

##### 2. **Delete the entire map**

```bash 
localhost:9219> MAP.DEL user-001:settings
Ok
```

Result: The entire `user-001:settings` entry is removed from memory.

***

#### Behavior on Error

| Error Condition           | Description                                                                               |
| ------------------------- | ----------------------------------------------------------------------------------------- |
| More than 2 arguments     | InvalidArgsError: More than 2 args not supported, Supported args Key or key and mapKey    |
| Invalid map key (field)   | InvalidMapKeyError:                                                                       |
| Value at key is not a map | InvalidValueError: The current value associated with the provided key must be a Map type. |

***

#### Additional Notes

* If the map contains only one key and that key is being deleted, the entire map will be removed automatically.

* If the map does not exist, the command will return `Ok` without performing any action.

 
