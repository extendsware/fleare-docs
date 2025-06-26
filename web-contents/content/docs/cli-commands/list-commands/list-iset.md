---
draft: false
title: LIST.ISET
is_title_visible: false
description: >-
  The LIST.ISET command allows users to insert or replace an element at a
  specified index in a list stored at the provided key. 
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline

date: '2025-06-20T15:54:55.178Z'
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
weight: 5000000
id: /documentations/cli-commands/list-commands/list-iset.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.526Z'
---
#### Command: `LIST.ISET` 

***

#### Overview

The `LIST.ISET` command allows users to insert or replace an element at a specified index in a list stored at the provided key. This operation is index-based, and it does **not** extend the list—an out-of-range index returns an error.

***

#### Command Name

**LIST.ISET**

#### Description

Sets the value at the specified index of a list. If the key does not exist and the index is zero, a new list is created with the element. For any other index on a non-existent list, or if the index is out of range for an existing list, the command returns an error.

#### Use Cases

* Replacing an element in a list at a known index.

* Initializing a list with the first element.

* Modifying a specific list entry based on zero-based index.

***

#### Syntax

```bash 
LIST.ISET <key> <index> <value>
```

*  `<key>` : A valid string key under which the list is stored.

*  `<index>` : A zero-based index at which to set the element.

*  `<value>` : The new value to store at the index. Can be any valid JSON value or string.

#### Permissions

* Read/Write access to the key space.

* Valid only for authenticated users if your system enforces auth.

* Must follow key naming and formatting rules.

***

#### Examples

##### Setting the first element

```bash 
localhost:9219> LIST.ISET myKey 0 "This is my first element"
Ok

localhost:9219> LIST.GET myKey
Ok [
  "This is my first element"
]
```

##### Setting another element in the same list

```bash 
localhost:9219> LIST.ISET myKey 1 "This is my second element"
Ok

localhost:9219> LIST.GET myKey 1
Ok "This is my second element"
```

#### Behavior on Error

| Condition                            | Error Message                                                                              |
| ------------------------------------ | ------------------------------------------------------------------------------------------ |
| No arguments                         |  `InvalidKeyError: Key must be provided`                                                   |
| Incorrect number of arguments        |  `InvalidArgsError: invalid number of arguments, Syntax: LIST.ISET <key> <index> <value>`  |
| Invalid index (non-integer or < 0)   |  `InvalidArgsError: Invalid index value. The index must be a number >= 0`                  |
| Index out of range for existing list |  `InvalidIndexError: index out of range`                                                   |
| Index > 0 on non-existing list       |  `InvalidIndexError: index out of range`                                                   |

 
