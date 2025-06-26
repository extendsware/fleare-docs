---
draft: false
title: NUM.INCR
is_title_visible: false
description: The NUM.INCR command increments a numeric value associated with a key.
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline

date: '2025-06-20T10:40:07.986Z'
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
id: /documentations/cli-commands/number-commands/num-incr.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.472Z'
---
#### Command: `NUM.INCR` 

***

#### Overview

The `NUM.INCR` command increments a numeric value associated with a key. If the key does not exist, it sets the key to the given value (or to 1 by default). This command supports both integer and floating-point numbers.

#### Command Name

 `NUM.INCR` 

***

#### Description

 `NUM.INCR` retrieves the value associated with a key, adds the specified increment (default is 1), and stores the result back. If the key does not exist, it initializes the key with the increment value. The command supports numeric data types only (integers and floats).

#### Use Cases

* Incrementing counters

* Tracking numerical metrics (e.g., page visits, scores)

* Performing atomic add operations in a concurrent environment

***

#### Syntax

```bash 
localhost:9219> NUM.INCR <key> [increment]
```

*  `<key>` : Required. The key whose value needs to be incremented.

*  `[increment]` : Optional. The numeric value to increment by. Defaults to `1` if omitted.

***

#### Permissions

* Write access to the specified key.

* Internal shard resolution and write-ahead log access are required.

***

#### Input Examples

##### Basic increment

```bash 
localhost:9219> NUM.SET myNumber 42
Ok

localhost:9219> NUM.INCR myNumber
Ok 43
```

##### Increment by specific value

```bash 
localhost:9219> NUM.INCR myNumber 10
Ok 53
```

##### Floating-point operations

```bash 
localhost:9219> NUM.SET myNumber 11.5
Ok

localhost:9219> NUM.INCR myNumber
Ok 12.5

localhost:9219> NUM.INCR myNumber 0.5
Ok 13
```

***

#### Output Examples

##### Example1

```bash 
localhost:9219> NUM.SET myNumber 42
Ok
```

##### Example2

```bash 
localhost:9219> NUM.INCR myNumber
Ok 43
```

##### Example3

```bash 
localhost:9219> NUM.INCR myNumber 10
Ok 53
```

##### Example4

```bash 
localhost:9219> NUM.SET myNumber 11.5
Ok
```

##### Example4

```bash 
localhost:9219> NUM.INCR myNumber
Ok 12.5
```

##### Example5

```bash 
localhost:9219> NUM.INCR myNumber 0.5
Ok 13
```

***

#### Behavior on Error

The command may fail in the following scenarios:

| Error Type            | Description                                                                     |
| --------------------- | ------------------------------------------------------------------------------- |
|  `InvalidKeyError`    | If the key is missing or not a valid key format                                 |
|  `InvalidArgsError`   | If more than 2 arguments are passed                                             |
|  `InvalidValueError`  | If the existing key is not numeric or the increment value is not a valid number |

 
