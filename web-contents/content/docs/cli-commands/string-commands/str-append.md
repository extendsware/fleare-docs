---
draft: false
title: STR.APPEND
is_title_visible: false
description: >-

  The STR.APPEND command is used to append one or more string values to an
  existing string stored at a given key.
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline
date: '2025-06-19T18:22:15.241Z'
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
weight: 1000000
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.482Z'
---
#### Command: `STR.APPEND` 

***

#### **Overview**

The `STR.APPEND` command is used to append one or more string values to an existing string stored at a given key. If the key does not exist, it creates a new entry with the concatenated value.

#### **Command Name**

 `STR.APPEND` 

#### **Description**

Appends the provided string values to the end of the string currently stored at the specified key. If the key does not exist, a new string is created. If the existing value is not a string, an error is returned.

#### **Use Cases**

##### Append Logging Entries

You can use `STR.APPEND` to build log-like string values that grow with each log message:

```bash 
STR.APPEND log:serviceA "[INFO] Started"
STR.APPEND log:serviceA " [DEBUG] Listening on port 8080"
```

##### Construct Responses

Build dynamic string responses over time based on state or input:

```bash 
STR.APPEND response:user42 "Hello "

STR.APPEND response:user42 "World"
```

##### Progressive Key Initialization

Initialize a new key and keep updating it in different steps:

```bash 
STR.APPEND init:flow "Step1"

STR.APPEND init:flow " -> Step2"
```

#### **Syntax**

```bash 
STR.APPEND <key> <value> [<value> ...]
```

*  `<key>` : Required. The key of the existing or new string.

*  `<value>` : One or more strings to append.

#### **Permissions**

* Read & Write access on the specified key.

* Internal shard lookup is based on the key for distributed storage compatibility.

***

#### **Input Examples**

##### Append to a non-existent key

```bash 
localhost:9219> STR.APPEND key1 "Hello"

Ok
```

##### Append to an existing key

```bash 
localhost:9219> STR.APPEND key1 " World"

Ok
```

##### Append multiple values

```bash 
localhost:9219> STR.APPEND key1 " and" " John"

Ok
```

***

#### **Output Examples**

##### After appending:

```bash 
localhost:9219> GET key1

Ok "Hello World and John"
```

***

#### **Behavior on Error**

| Error Condition                               | Message                                                                         |
| --------------------------------------------- | ------------------------------------------------------------------------------- |
| No key provided                               |  `InvalidKeyError: Key must be provided`                                        |
| Key name fails validation                     |  `InvalidKeyError: <validation reason>`                                         |
| Value at key is not of type `string`          |  `InvalidValueError: the existing value for the provided key must be a string`  |
| Storage backend error while setting the value |  `<error from store.M.Set>`                                                     |


 
