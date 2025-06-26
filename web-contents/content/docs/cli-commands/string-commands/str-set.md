---
draft: false
title: STR.SET
is_title_visible: false
description: >-
  The STR.SET command stores or updates a string value associated with a
  specified key. 
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline

date: '2025-06-18T18:56:43.873Z'
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
weight: 3000000
id: /documentations/cli-commands/string-commands/str-set.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.485Z'
---
#### Command: `STR.SET` 

***

#### **Overview**

The `STR.SET` command stores or updates a string value associated with a specified key. If the key already exists, its value is overwritten.

#### **Command Name**

 `STR.SET` 

#### **Description**

 `STR.SET` is used to store a string data item under a key. If the key already exists, its value will be overwritten with the new string. This command is part of the string operations in the Fleare database engine.

#### **Use Cases**

1. **Basic String Storage**

   * Use `STR.SET` to initialize a key with a string value (e.g., `"Welcome"` ).

2. **Update Existing Key**

   * Store dynamic strings like `"SessionToken"` , `"GreetingMessage"` , or `"Status"` by updating them with `STR.SET` .

3. **Command in Automation Scripts**

   * Automate inserting default configuration or cache values during service start-up.

4. **Storing Logs or Short Status Messages**

   * Use for quick updates like `STR.SET service:health "OK"` or `STR.SET user:123:state "active"` .

#### **Syntax**

```bash 
STR.SET <key> <value>
```

*  `<key>` : The key under which the value will be stored (must be a valid string key).

*  `<value>` : The string value to store (can include spaces if quoted).

#### **Permissions**

* Write access is required to the target keyspace/shard.

* No special roles or privileges are required beyond basic write permissions.

***

#### **Input Examples**

##### Example 1: Basic Set

```bash 
localhost:9219> STR.SET user:greeting "Hello"
```

Stores `"Hello"` under key `user:greeting` .

##### Example 2: Overwrite Existing Key

```bash 
localhost:9219> STR.SET user:greeting "World World"
```

Overwrites the previous value ( `"Hello"` ) with `"World World"` .

***

#### **Output Examples**

##### Successful Set

```bash 
localhost:9219> STR.SET user:greeting "Hello"
Ok
```

##### Overwrite with New Value

```bash 
localhost:9219> STR.SET user:greeting "World World"
Ok
```

##### Verification with GET

```bash 
localhost:9219> GET user:greeting
Ok "World World"
```

***

#### **Behavior on Error**

| Condition                        | Error Message                                     |
| -------------------------------- | ------------------------------------------------- |
| Missing arguments                |  `InvalidKeyError: invalid number of arguments`  |
| Missing key                      |  `InvalidKeyError: Key must be provided`          |
| Invalid key format (e.g., empty) |  `InvalidKeyError: <reason>`                      |

 
