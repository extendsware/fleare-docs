---
draft: false
title: LIST.LEN
is_title_visible: false
description: >-
  The LIST.LEN command is used to retrieve the number of elements in a list
  stored at a given key. 
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline

date: '2025-06-20T13:07:02.537Z'
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
id: /documentations/cli-commands/list-commands/list-len.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.506Z'
---
#### Command: `LIST.LEN` 

***

#### Overview

The `LIST.LEN` command is used to retrieve the number of elements in a list stored at a given key. It validates the key, checks for the appropriate data type, and returns the size of the list. If the key is not associated with a list, or if the key doesn't exist, a relevant error or response is returned.

#### Command Name

 `LIST.LEN` 

#### Description

Returns the length of the list stored at the specified key.

* If the key does not exist, the command returns `0` .

* If the key exists but is not a list, an error is returned.

* Supports validation for proper key format.

#### Use Cases

1. **Monitoring list sizes**: Determine how many items are currently queued or stored.

2. **Pre-validation before iteration**: Check if a list contains any elements before processing.

3. **Debugging data structure issues**: Confirm the data structure associated with a key is a list and inspect its length.

4. **Efficient length retrieval**: Avoid fetching the entire list for size checks.

***

#### Syntax

```bash 
LIST.LEN <key>
```

*  `<key>` : The name of the list key to query.

***

#### Permissions

* Read access is sufficient.

* No special permissions required beyond access to the key.

***

#### Examples

**Example 1: Successful Retrieval**

```bash 
localhost:9219> LIST.ISET myKey 0 "This is my first element"
Ok

localhost:9219> LIST.ISET myKey 1 "{"name":"John", "address": "kolkata"}"
Ok

localhost:9219> LIST.LEN myKey
Ok 2
```

**Example 2: Key Does Not Exist**

```bash 
localhost:9219> LIST.LEN unknownKey
Ok 0
```

**Example 3: Key Is Not a List**

```bash 
localhost:9219> SET myKey "not a list"
Ok

localhost:9219> LIST.LEN myKey
InvalidValueError: The current value associated with the provided key must be a list
```

**Example 4: Invalid Arguments**

```bash 
localhost:9219> LIST.LEN
InvalidKeyError: Key must be provided
```

***

#### Behavior on Error

| Scenario                       | Error Message                                                                            |
| ------------------------------ | ---------------------------------------------------------------------------------------- |
| No key provided                |  `InvalidKeyError: Key must be provided`                                                 |
| Incorrect number of arguments  |  `InvalidArgsError: invalid number of arguments, Syntax: LIST.LEN <key>`                 |
| Invalid key format             |  `InvalidKeyError: <reason>`                                                             |
| Key not associated with a list |  `InvalidValueError: The current value associated with the provided key must be a list`  |


 
