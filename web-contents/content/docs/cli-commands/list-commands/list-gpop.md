---
draft: false
title: LIST.GPOP
is_title_visible: false
description: >-
  The LIST.GPOP Removes and returns the last element from the list stored at the
  specified key.

date: '2025-06-20T16:02:43.069Z'
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
id: /documentations/cli-commands/list-commands/list-gpop.md
weight: 1000000
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.503Z'
---
#### Command: `LIST.GPOP` 

***

#### Overview

The `LIST.GPOP` command is used to **remove and return the last (most recently pushed) element** from a list stored at the given key. It behaves like a `POP` operation in a list, specifically removing the element at the end (LIFO order) while also returning it to the user.

***

#### Command Name

 `LIST.GPOP` 

#### Description

Removes and returns the **last element** from the list stored at the specified key.

* If the key does not exist, it returns an empty response.

* If the key exists but the value is not a list, an error is thrown.

* If the list is empty, an error is thrown.

* Preserves the list state after removing the last item.

#### Use Cases

* Implementing a task stack where the most recent task needs to be popped for processing.

* Managing temporary storage where the last inserted value must be retrieved and removed.

* Stack-like operations in workflows, e.g., undo buffers or processing queues.

#### Syntax

```bash 
LIST.GPOP <key>
```

*  `<key>` : The identifier of the list.

#### Permissions

* **Read & Write** access required on the specified key.

* Only users or systems with permission to **mutate list data** should be allowed to execute `LIST.GPOP` .

***

#### Examples

##### Example 1: Basic Use

```bash 
localhost:9219> LIST.PUSH myList "hello"
Ok
localhost:9219> LIST.PUSH myList "world"
Ok
```

```bash 
localhost:9219> LIST.GPOP myList
Ok "world"
```

```bash 
localhost:9219> LIST.GET myList
Ok [
  "hello"
]
```

##### Example 2: Pop JSON Objects and Numbers

```bash 
localhost:9219> LIST.PUSH myKey "string value"
Ok

localhost:9219> LIST.PUSH myKey '{"name":"Alice","city":"Delhi"}' 99.9
Ok
```

```bash 
localhost:9219> LIST.GPOP myKey
Ok 99.9
```

```json 
localhost:9219> LIST.GET myKey
Ok [
  "string value",
  {
    "name": "Alice",
    "city": "Delhi"
  }
]
```

##### Example 3: Pop a Boolean Value

```bash 
localhost:9219> LIST.PUSH flags true false
Ok

localhost:9219> LIST.GPOP flags
Ok false

localhost:9219> LIST.GET flags
Ok [
  true
]
```

##### Example 4: Pop From a List with Only One Element

```bash 
localhost:9219> LIST.PUSH singleList "only"
Ok

localhost:9219> LIST.GPOP singleList
Ok "only"

localhost:9219> LIST.GET singleList
Ok []
```

##### Example 5: Pop from List with Nested JSON

```bash 
localhost:9219> LIST.PUSH users '{"id":1,"data":{"name":"John","age":30}}'
Ok

localhost:9219> LIST.PUSH users '{"id":2,"data":{"name":"Jane","age":25}}'
Ok
```

```json 
localhost:9219> LIST.GPOP users
Ok {
  "id": 2,
  "data": {
    "name": "Jane",
    "age": 25
  }
}

localhost:9219> LIST.GET users
Ok [
  {
    "id": 1,
    "data": {
      "name": "John",
      "age": 30
    }
  }
]
```

##### Example 6: Pop Mixed-Type List (string, number, JSON)

```bash 
localhost:9219> LIST.PUSH mix "text" 42 '{"x": 1}'
Ok
```

```json 
localhost:9219> LIST.GPOP mix
Ok {
  "x": 1
}

localhost:9219> LIST.GET mix
Ok [
  "text",
  42
]
```

##### Example 7: Attempting to GPOP from Non-List Key

```bash 
localhost:9219> SET notAList "hello"
Ok

localhost:9219> LIST.GPOP notAList
Error: InvalidValueError: the existing value for the provided key must be a list
```

***

#### Behavior on Error

| Error Condition                    | Error Message Example                                                                              |
| ---------------------------------- | -------------------------------------------------------------------------------------------------- |
| No key provided                    |  `InvalidKeyError: Key must be provided`                                                         |
| Key exists but value is not a list |  `InvalidValueError: the existing value for the provided key must be a list`                     |
| List is empty or has no elements   |  `InvalidKeyError: index out of range [last] with length 0`                                      |

***

#### Return Value

* The **last element** from the list is returned and removed from the list.
* If it's a JSON object, it's returned in structured format.
* If it's a primitive (string, number), it is returned as-is.#
   
