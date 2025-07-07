---
draft: false
title: LIST.GET
is_title_visible: false
description: >-
  The LIST.GET command retrieves one or more elements from a list stored at a
  specific key. 

date: '2025-06-20T16:36:27.451Z'
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
id: /documentations/cli-commands/list-commands/list-get.md
weight: 6000000
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.507Z'
---
#### Command: `LIST.GET` 

***

#### Overview

The `LIST.GET` command retrieves one or more elements from a list stored at a specific key. If an index is provided, it returns the value at that index; otherwise, it returns the entire list.

#### Command Name

 `LIST.GET` 

***

#### Description

Fetches the list element(s) stored under a given key:

* If only the key is provided, the full list is returned.

* If a specific index is given, only the item at that index is returned.

* An error is thrown if the index is out of bounds or the value at the key is not a list.

#### Use Cases

* Retrieve the entire list for display or processing.

* Access a specific item in the list using its index.

* Validate list contents during debugging or runtime checks.

#### Syntax

```bash 
LIST.GET <key> [index]
```

*  `<key>` – The name of the key where the list is stored. **(Required)**

*  `[index]` – The optional position of the list item to retrieve (0-based index).

***

#### Permissions

* The user must have **read** access to the key.

* The key must exist and point to a list-type value.

***

#### Examples

##### Retrieve Full List

```bash 
localhost:9219> LIST.SET myKey 0 "This is my first element"
Ok

localhost:9219> LIST.SET myKey 1 "{"name":"John", "address": "kolkata"}"
Ok

localhost:9219> LIST.GET myKey
Ok [
  "This is my first element",
  {"name":"John", "address": "kolkata"}
]
```

##### Retrieve Specific Index

```json 
localhost:9219> LIST.GET myKey 1
Ok {
  "name":"John", 
  "address": "kolkata"
}
```

***

#### Behavior on Error

| Scenario                     | Error Type            | Message                                                               |
| ---------------------------- | --------------------- | --------------------------------------------------------------------- |
| Key not provided             |  `InvalidKeyError`    |  `Key must be provided`                                               |
| Too many arguments           |  `InvalidArgsError`   |  `invalid number of arguments`                                        |
| Key exists but not a list    |  `InvalidValueError`  |  `The current value associated with the provided key must be a list`  |
| Index is not a valid integer |  `InvalidArgsError`   |  `Invalid index value. The index must be a number ≥ 0`                |
| Index is out of bounds       |  `InvalidIndexError`  |  `index out of range`                                                 |

 
