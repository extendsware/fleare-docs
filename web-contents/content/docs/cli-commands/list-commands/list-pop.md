---
draft: false
title: LIST.POP
is_title_visible: false
description: >-
  The LIST.POP command removes (pops) a single element from the beginning (index
  0) of a list stored at a specified key. If the list becomes empty after the
  pop, the key is removed from the store.
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline

date: '2025-06-20T12:40:31.779Z'
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
weight: 8000000
id: /documentations/cli-commands/list-commands/list-pop.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.520Z'
---
#### Command: `LIST.POP` 

***

#### Overview

The `LIST.POP` command return (pops) a single element from the **beginning** (index 0) of a list stored at a specified key. If the list becomes empty after the pop, the key is removed from the store.

#### Command Name

 `LIST.POP` 

#### Description

Removes the first element from a list stored at the provided key.

* If the list contains more than one item, only the first is removed.

* If it contains exactly one item, the entire key is deleted.

* If the key doesn't exist, the command returns an empty result.

* If the key exists but is not a list, an error is returned.

#### Use Cases

* **Queue-like processing**: Use `LIST.POP` to process tasks from a list where items are inserted using `LIST.PUSH` .

* **FIFO data consumption**: Retrieve data in a First-In-First-Out manner.

* **Cleaning up data**: Automatically delete keys when lists become empty.

* **Lightweight job scheduler**: Pop jobs/tasks from a list stored under a worker queue.

***

#### Syntax

```bash 
LIST.POP <key>
```

*  `<key>` : The key associated with the list from which to remove the first item.

***

#### Permissions

No special permissions are required to execute this command. However, the caller must have:

* Access to the given key.

* Write privileges on the key's shard.

***

#### Examples

##### Example 1: Pop from a list with multiple values

```bash 
localhost:9219> LIST.PUSH myKey "First"
Ok

localhost:9219> LIST.PUSH myKey "Second" "Third"
Ok
```

```bash 
localhost:9219> LIST.POP myKey
Ok "First"
```

##### Example 2: Pop from a list with one value (deletes the key)

```bash 
localhost:9219> LIST.PUSH myKey "OnlyOne"
Ok

localhost:9219> LIST.POP myKey
Ok "OnlyOne"
```

##### Example 3: Pop from a nonexistent key

```bash 
localhost:9219> LIST.POP unknownKey
Ok
```

*Note: Output is intentionally minimal. Use `LIST.GET <key>` afterward to verify changes.*

##### After popping, the remaining list:

```bash 
localhost:9219> LIST.GET myKey
Ok [
  "Second",
  "Third"
]
```

##### When key does not exist:

```bash 
Ok
```

##### When key contains invalid (non-list) data:

```bash 
InvalidValueError: the existing value for the provided key must be a list
```

##### When key is not provided:

```bash 
InvalidKeyError: Key must be provided
```

***

#### Behavior on Error

| Scenario                            | Error Message                                                                   |
| ----------------------------------- | ------------------------------------------------------------------------------- |
| No key provided                     |  `INVALID_KEY_ERROR: Key must be provided`                                      |
| Invalid key format (non-conforming) |  `INVALID_KEY_ERROR: <validation error>`                                        |
| Value at key is not of list type    |  `INVALID_VALUE_ERROR: the existing value for the provided key must be a list`  |
| Malformed JSON stored in list       |  `INVALID_CHARACTER_ERROR: <JSON unmarshal error>`                              |

 
