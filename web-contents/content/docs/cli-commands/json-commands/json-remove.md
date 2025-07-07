---
draft: false
title: JSON.REMOVE
is_title_visible: false
description: >-
  The JSON.REMOVE command allows users to delete a specific field or the entire
  JSON object associated with a key stored in the Fleare in-memory database.
date: '2025-06-22T15:43:33.565Z'
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
  last_published: '2025-06-23T15:58:21.607Z'
is_summary_visible: true
is_taxonomy_visible: true
is_folder_visible_in_listing: false
weight: 6000000
id: /documentations/cli-commands/json-commands/json-remov.md
---
#### Command: `JSON.REMOVE` 

***

#### Overview

The `JSON.REMOVE` command allows users to delete a specific field or the entire JSON object associated with a key stored in the Fleare in-memory database. It supports nested paths using dot notation and ensures safe deletion based on key validation and type checking.

#### Command Name

**`JSON.REMOVE`**

#### Description

Removes a specific path or the entire JSON object associated with the given key.

* If only the key is provided, the whole JSON value is deleted.

* If a path is specified (including nested fields using dot notation), only that field is removed from the JSON structure.

#### Use Cases

* Deleting an entire JSON object by key.

* Removing a top-level key (e.g., `isActive` ) from a JSON object.

* Removing nested fields (e.g., `address.city` ) without affecting the rest of the JSON.

* Cleaning up or pruning unnecessary data from stored objects.

***

#### Syntax

```bash 
JSON.REMOVE <key> [<path>]
```

*  `<key>` (string) – Required. The key associated with the JSON object.

*  `<path>` (string) – Optional. The path of the field to remove using dot notation (e.g., `address.city` ).

#### Permissions

* Requires **read-write** access to the specified key.

* Key must exist and must be of type `JSON` .

***

#### Examples

##### 1. Remove entire JSON object

```bash 
localhost:9219> JSON.SET user '{"name":"Alice","age":25}'
Ok

localhost:9219> JSON.REMOVE user
Ok
```

##### 2. Remove a top-level field

```bash 
localhost:9219> JSON.SET profile '{"name":"Bob","active":true,"score":42}'
Ok
```
```bash 
localhost:9219> JSON.REMOVE profile "active"
Ok {
  "name": "Bob",
  "score": 42
}
```

##### 3. Remove a nested field

```bash 
localhost:9219> JSON.SET account '{"user":{"id":1,"email":"bob@example.com"},"status":"active"}'
Ok

localhost:9219> JSON.REMOVE account "user.email"
Ok {
  "user": {
    "id": 1
  },
  "status": "active"
}
```

##### 4. Remove a non-existent nested field (no error, returns original)

```bash 
localhost:9219> JSON.REMOVE account "user.phone"
Ok {
  "user": {
    "id": 1
  },
  "status": "active"
}
```

***

#### Behavior on Error

| Scenario                   | Error Message                                                                                   |
| -------------------------- | ----------------------------------------------------------------------------------------------- |
| Missing key argument       |  `InvalidKeyError: Key must be provided`                                                        |
| Invalid key format         |  `InvalidKeyError: <details>`                                                                   |
| Key not found              | Returns empty response (no error)                                                               |
| Value is not a JSON object |  `InvalidValueError: The current value associated with the provided key must be a json object`  |
| Malformed JSON value       |  `InvalidCharacterError: <unmarshal error details>`                                             |
| Invalid path structure     |  `invalid path: <path>`                                                                         |

***

 
