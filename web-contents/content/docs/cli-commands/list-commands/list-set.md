---
draft: false
title: LIST.SET
is_title_visible: false
description: >-
  The LIST.SET command clears the existing elements associated with a given list
  key and sets the provided values as the new list elements.
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline

date: '2025-06-19T16:45:04.593Z'
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
weight: 2000000
id: /documentations/cli-commands/list-commands/list-set.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.504Z'
---
#### Command: `LIST.SET` 

***

#### Overview

The `LIST.SET` command clears the existing elements associated with a given list key and sets the provided values as the new list elements. It effectively replaces any previously stored data under the key with the new list.

#### Command Name

**LIST.SET**

#### Description

Replaces all elements in a list with new ones provided during the call. This command clears existing contents at the specified key and sets the new list items from the input. Returns the number of elements added to the list (as an index count).

#### Use Cases

* **Replace existing list data**: Ideal when a complete list reset is required for a given key.

* **Atomic overwrite of list**: Ensures old list values are cleared and new ones are inserted in a single operation.

* **Staging or configuration reset**: Useful for overwriting cached configurations, logs, or batch records.

***

#### Syntax

```bash 
LIST.SET <key> [<value>...]
```

*  `<key>` : The name of the list where the data will be set.

*  `<value>` : One or more elements to be inserted into the list.

**Note**: If the key is invalid or the argument list is insufficient, an error is returned.

***

#### Permissions

Requires write access to the given key.

***

#### Examples

##### Example 1 – Single element

```bash 
localhost:9219> LIST.SET myList "First element"
Ok 1
```

##### Example 2 – Multiple elements

```bash 
localhost:9219> LIST.SET myList "First" "Second" "Third"
Ok 3
```

##### Retrieve elements

```json 
localhost:9219> LIST.GET myList
Ok [
    "First",
    "Second",
    "Third"
]
```

***

#### Behavior on Error

| Scenario                              | Error Message                                                                   |
| ------------------------------------- | ------------------------------------------------------------------------------- |
| No key provided                       |  `INVALID_KEY: Key must be provided`                                            |
| Less than 2 arguments (missing value) |  `INVALID_ARGS: invalid number of arguments, Syntax: LIST.SET <key> [<value>]`  |
| Invalid key format                    |  `INVALID_KEY: <error description>`                                             |
| Internal store error                  |  `<error returned by the shard or WAL>`                                         |

 
