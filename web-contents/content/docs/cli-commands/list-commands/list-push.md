---
draft: false
title: LIST.PUSH
is_title_visible: false
description: >-
  The LIST.PUSH command inserts one or more elements at the beginning of a list
  associated with a specific key in the Fleare in-memory database.
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline

date: '2025-06-20T11:55:36.088Z'
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
weight: 7000000
id: /documentations/cli-commands/list-commands/list-push.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.510Z'
---
#### Command: `LIST.PUSH` 

***

#### Overview

The `LIST.PUSH` command inserts one or more elements at the beginning of a list associated with a specific key in the Fleare in-memory database. If the key does not exist, a new list is created. If the key exists but holds a non-list data type, an error is returned.

#### Command Name

 `LIST.PUSH` 

#### Description

This command prepends one or more elements to the beginning of a list stored at the given key.

* If the key is **not present**, a **new list** is created and the elements are inserted.

* If the key **exists but does not represent a list**, an **error is thrown**.

* Elements can be of various types: strings, numbers, and valid JSON objects.

#### Use Cases

* Prepend messages to a user notification list

* Maintain a history of API call payloads

* Store numeric logs with real-time data

***

#### Syntax

```bash 
LIST.PUSH <key> <element> [<element>...]
```

*  `<key>` : A valid string representing the name of the list.

*  `<element>` : One or more values to be inserted at the beginning of the list. These can be plain strings, numbers, or JSON strings.

***

#### Permissions

* Read and write access to the specified key’s shard.

* Permission to modify the Write-Ahead Log (WAL).

***

#### Examples

```bash 
localhost:9219> LIST.PUSH myKey "This is my first element"
Ok

localhost:9219> LIST.PUSH myKey '{"name":"John", "address": "kolkata"}' 10023.22
Ok
```

```bash 
localhost:9219> LIST.GET myKey
```

```json 
Ok [
  "This is my first element",
  {
    "name": "John",
    "address": "kolkata"
  },
  10023.22
]
```

##### Inserting multiple string elements

```bash 
localhost:9219> LIST.PUSH fruits "apple" "banana" "cherry"
Ok
```

##### Inserting a mix of JSON, number, and string

```bash 
localhost:9219> LIST.PUSH data '{"user":"alice"}' 42 "note"
Ok
```

##### Inserting a JSON array as a single element

```bash 
localhost:9219> LIST.PUSH complexList '[1, 2, 3]'
Ok
```

*Note: This inserts the **whole array as a single element**, not three separate values.*

##### Example 4: Creating a list at a new key

```bash 
localhost:9219> LIST.PUSH newList "firstItem"
Ok
```

##### Unicode and special characters

```bash 
localhost:9219> LIST.PUSH greetings "こんにちは" "¡Hola!" "Cześć"
Ok
```

##### For LIST.GET fruits

```json 
localhost:9219> LIST.GET fruits
Ok [
  "apple",
  "banana",
  "cherry"
]
```

##### For LIST.GET data

```json 
localhost:9219> LIST.GET data
Ok [
  {
    "user": "alice"
  },
  42,
  "note"
]
```

##### For LIST.GET complexList

```json 
localhost:9219> LIST.GET complexList
Ok [
  [
    1,
    2,
    3
  ]
]
```

##### For LIST.GET greetings

```json 
localhost:9219> LIST.GET greetings
Ok [
  "こんにちは",
  "¡Hola!",
  "Cześć"
]
```

***

## Behavior on Error

| Scenario                   | Error Message                                        |
| -------------------------- | ---------------------------------------------------- |
| No key provided            |  `ERR_INVALID_KEY: Key must be provided`             |
| Invalid characters in key  |  `ERR_INVALID_KEY: <detailed validation error>`      |
| Existing key is not a list |  `ERR_INVALID_CHARACTER: <unmarshal error message>`  |
| Storage write failure      |  `Error returned from shard.M.Set()`                 |

 
