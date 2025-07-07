---
draft: false
title: STR.GET
is_title_visible: false
description: >-
  The STR.GET command is used to retrieve the string value associated with a
  specified key.

date: '2025-06-19T18:55:04.308Z'
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
weight: 4000000
id: /documentations/cli-commands/string-commands/str-get.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.488Z'
---
#### Command: `STR.GET` 

***

#### **Overview**

The `STR.GET` command is used to retrieve the string value associated with a specified key. If the key does not exist or has a different data type, appropriate responses are returned. This command is safe to use for read-only operations and ensures type safety for string keys.

#### **Command Name**

 `STR.GET` 

#### **Description**

Retrieves the string value stored at the specified key. If the key exists and holds a string, the value is returned. If the key does not exist, an empty string is returned. If the key holds a non-string type (e.g., list, set, etc.), an error is returned.


#### **Use Cases**

##### Read from cache/store

To retrieve a value previously stored using `STR.SET` , e.g., fetching user session token or a config value.

##### Fallback handling

To check whether a key exists or needs initialization:

```bash 
if STR.GET mykey == ""
   then STR.SET mykey "default_value"
```

#### **Syntax**

```bash 
STR.GET <key>
```

*  `<key>` – The key whose associated string value is to be retrieved.

#### **Permissions**

* No special permissions required.

* The client must have read access to the key's shard.

***

#### **Input Examples**

##### Existing Key with String

```bash 
localhost:9219> STR.SET greeting "Hello, World"
Ok

localhost:9219> STR.GET greeting
Ok "Hello, World"
```

##### Non-Existing Key

```bash 
localhost:9219> STR.GET missing_key
Ok ""
```

##### Invalid Example: Missing Key Argument

```bash 
localhost:9219> STR.GET
Error: ERR_INVALID_KEY: Key must be provided
```

##### Invalid Example: More Than One Argument

```bash 
localhost:9219> STR.GET key1 key2
Error: ERR_INVALID_ARGS: invalid number of arguments
```

##### Invalid Example: Wrong Data Type

```bash 
localhost:9219> LIST.APPEND mylist "value"
Ok

localhost:9219> STR.GET mylist
Error: ERR_INVALID_VALUE: the existing value for the provided key must be a string
```

***

#### **Output Examples**

| Case                    | Output                       |
| ----------------------- | ---------------------------- |
| Existing key            |  `Ok "value"`                |
| Non-existing key        |  `Ok ""`                     |
| Invalid key (empty)     |  `Error: ERR_INVALID_KEY`    |
| Wrong type (not string) |  `Error: ERR_INVALID_VALUE`  |
| Wrong arg count         |  `Error: ERR_INVALID_ARGS`   |

***

#### **Behavior on Error**

| Error Type            | Cause                                        | Message                                     |
| --------------------- | -------------------------------------------- | ------------------------------------------- |
|  `ERR_INVALID_KEY`    | No key provided or invalid characters in key |  `Key must be provided` or key format issue |
|  `ERR_INVALID_ARGS`   | More or fewer than one argument              |  `invalid number of arguments`              |
|  `ERR_INVALID_VALUE`  | Key exists but value is not of type string   |  `the existing value must be a string`      |

Errors are returned with a consistent `Error:` prefix and proper error codes for easier automation.

***

##### Key validation

To ensure the key points to a valid string value before performing string operations.

 
