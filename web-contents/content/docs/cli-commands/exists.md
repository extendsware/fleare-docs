---
draft: false
title: EXISTS
is_title_visible: false
description: >-
  The EXISTS command is used to verify the existence of one or more keys in the
  database.
cover_image: 'https://www.bakemyweb.com/preview1/docs.fleare.com/box.png'
date: '2025-06-18T17:45:32.565Z'
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
weight: 6000000
id: /documentations/cli-commands/exists.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T20:35:27.641Z'
---
#### Command: `EXISTS` 

***

#### Overview

The `EXISTS` command is used to verify the existence of one or more keys in the database. It returns the count of keys that exist from the list provided.

#### Command Name

**EXISTS**

#### Description

Checks whether each provided key exists in the current database. The result is the number of keys that are found.

#### Syntax

```bash 
EXISTS <key> [<key> ...]
```

*  `<key>` : A string key to check for existence. You can provide multiple keys separated by space.

#### Permissions

* **Read-only** command.

* Requires no special privileges.

* Any authenticated client can use this command.

##### Input Examples

##### Example 1: Single key check

```bash 
localhost:9219> EXISTS key1
```

##### Example 2: Multiple keys check

```bash 
localhost:9219> EXISTS key1 key2 key3
```

##### Output Examples

##### Example 1:

```bash 
Ok 1
```

*(Indicates that one of the keys exists.)*

##### Example 2:

```bash 
Ok 2
```

*(Indicates that two of the provided keys exist.)*

***

#### Behavior on Error

#### Missing argument:

```bash 
localhost:9219> EXISTS
```

**Response:**

```bash 
Error: InvalidKeyError: Key must be provided
```

* If no key is supplied, the command returns an `InvalidKeyError` .

* No partial processing is done—error occurs before any checking.

***

#### Use Cases

##### Use Case 1: Pre-check before GET/SET

Before performing an expensive `GET` or `UPDATE` , a user may want to confirm whether a key exists:

```bash 
EXISTS user:12345
```

##### Use Case 2: Bulk existence check

For cache population or eviction logic, checking which of a set of keys exist:

```bash 
EXISTS session:abc123 session:def456 session:xyz789
```

##### Use Case 3: Key health monitoring

Used by monitoring tools to check the presence of important heartbeat or sentinel keys.

 
