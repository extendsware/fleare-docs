---
draft: false
title: NUM.GET
is_title_visible: false
description: >-
  The NUM.GET command retrieves a numerical value (integer or float) from the
  database associated with the given key. 

date: '2025-06-20T07:54:38.243Z'
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
id: /documentations/cli-commands/number-commands/num-get.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.473Z'
---
#### Command: `NUM.GET` 

***

#### **Overview**

The `NUM.GET` command retrieves a numerical value (integer or float) from the database associated with the given key. It only supports keys whose values are of type `Number` . If the key does not exist or the value is not a number, an appropriate error is returned.

#### **Command Name**

 `NUM.GET` 

#### **Description**

This command fetches and returns the numeric value stored under a given key. It is useful for retrieving data that was previously set using numeric commands like `NUM.SET` . Only numeric values are allowed; if the value stored under the key is not a number, an error will be thrown.


#### **Use Cases**

* **Monitor counters or metrics**: Retrieve system or user-generated counters.

* **Arithmetic workflows**: Read the latest numeric value before performing further computations or updates.

* **Validation check**: Ensure that the value associated with a key is of numeric type before proceeding with operations that require numbers.

***

#### **Syntax**

```bash 
NUM.GET <key>
```

*  `<key>` : The key whose associated numeric value is to be retrieved. It must be a valid key format as per system validation rules.

***

#### **Permissions**

* **Read access** is required to query the key-value store.

* The user must have access to the shard containing the key.

* The key must exist and point to a value of numeric type.

***

#### **Input Examples**

```bash 
localhost:9219> NUM.SET myNumber 42
Ok

localhost:9219> NUM.GET myNumber
Ok 42

localhost:9219> NUM.SET myFloat 11.5
Ok

localhost:9219> NUM.GET myFloat
Ok 11.5
```

***

#### **Output Examples**

Successful outputs:

```bash 
Ok 42
```

```bash 
Ok 11.5
```

#### **Behavior on Error**

| Error Type        | Cause                                       | Message                                                                     |
| ----------------- | ------------------------------------------- | --------------------------------------------------------------------------- |
|  `invalid_key`    | Key is not provided or fails validation     |  `invalid_key: Key must be provided` or validation message                  |
|  `invalid_args`   | Command has more or fewer than one argument |  `invalid_args: invalid number of arguments`                                |
|  `invalid_value`  | Key exists but value is not a number        |  `invalid_value: the existing value for the provided key must be a number`  |


 
