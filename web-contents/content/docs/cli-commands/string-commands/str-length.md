---
draft: false
title: STR.LENGTH
is_title_visible: false
description: >-
  The STR.LENGTH command is used to retrieve the length (in characters) of a
  string value
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline

date: '2025-06-19T18:40:52.554Z'
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
id: /documentations/cli-commands/string-commands/str-length.md
weight: 5000000
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.489Z'
---
#### Command: `STR.LENGTH` 

***

#### Overview

The `STR.LENGTH` command is used to retrieve the length (in characters) of a string value stored at a specified key in the Fleare key-value store. If the key does not exist, it returns 0. It validates the key and ensures the value is of string type.

#### Command Name

 `STR.LENGTH` 

***

#### Description

This command returns the number of characters in the string value stored at the given key.

* If the key does not exist, it returns `0` .

* If the key exists but is associated with a non-string value, an error is returned.

* This command is **read-only** and does not modify any data.


#### Use Cases

##### Monitoring String Length
You can verify the size of messages, configurations, or serialized data before parsing.
##### Existence Check
Used to check if a key holds a value or not. If length `0` is returned, the key might not exist.
##### Validation Logic
Before processing, validate minimum or maximum required length of the value.

#### Syntax

```bash 
STR.LENGTH <key>
```

*  `<key>` : The key for which the string length is to be retrieved.

#### Permissions

* **Read** access required to the specified key.

* No special or elevated privileges needed.

***

#### Input Examples

##### Key exists with a string value

```bash 
localhost:9219> STR.SET greeting "Hello, Fleare"
Ok

localhost:9219> STR.LENGTH greeting
Ok 13
```

##### Key does not exist

```bash 
localhost:9219> STR.LENGTH unknown_key
Ok 0
```

##### Value is not a string

```bash 
localhost:9219> LIST.RPUSH mylist "one"
Ok

localhost:9219> STR.LENGTH mylist
ERR: invalid value: the existing value for the provided key must be a string
```

***

#### Output Examples

| Case                     | Output          |
| ------------------------ | --------------- |
| Valid string key         |  `Ok <length>`  |
| Non-existing key         |  `Ok 0`         |
| Value is not string type |  `ERR: ...`     |

***

#### Behavior on Error

| Condition                   | Error Message                                                                    |
| --------------------------- | -------------------------------------------------------------------------------- |
| No key provided             |  `ERR: invalid key: Key must be provided`                                        |
| Too many/few arguments      |  `ERR: invalid arguments: invalid number of arguments`                           |
| Key format is invalid       |  `ERR: invalid key: <validation error>`                                          |
| Value is not of string type |  `ERR: invalid value: the existing value for the provided key must be a string`  |

 
