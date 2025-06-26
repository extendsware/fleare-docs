---
draft: false
title: NUM.SET
is_title_visible: false
description: >-
  The NUM.SET command stores a numeric value (integer or floating-point) in the
  key-value database.
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline

date: '2025-06-20T07:47:04.811Z'
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
id: /documentations/cli-commands/number-commands/num-set.md
weight: 1000000
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.471Z'
---
#### Command: `NUM.SET` 

***

#### **Overview**

The `NUM.SET` command stores a numeric value (integer or floating-point) in the key-value database. This command is designed to handle numerical data efficiently.

***

#### **Command Name**

 `NUM.SET` 

***

#### **Description**

Stores a numeric value under a specific key in the database. The value can be any valid number format such as `int` , `float32` , or `float64` . If the key already exists, its value is overwritten.

#### **Syntax**

```bash 
NUM.SET <key> <value>
```

*  `<key>` : A valid string identifier where the number will be stored.

*  `<value>` : A valid numeric value (integer or float).

#### **Permissions**

* No special permissions are required to execute this command.

* Users must have access to the shard where the key is mapped.

***

#### **Input Examples**

```bash 
localhost:9219> NUM.SET myInt 42
Ok

localhost:9219> NUM.SET pi 3.14159
Ok

localhost:9219> NUM.SET balance -99.75
Ok
```

***

#### **Output Examples**

```bash 
localhost:9219> NUM.SET myInt 42
Ok

localhost:9219> GET myInt
Ok 42

localhost:9219> NUM.SET balance -99.75
Ok

localhost:9219> GET balance
Ok -99.75
```

***

#### **Behavior on Error**

| Error Scenario                | Error Message                                               |
| ----------------------------- | ----------------------------------------------------------- |
| No key provided               |  `InvalidKeyError: Key must be provided`                    |
| Incorrect number of arguments |  `InvalidArgsError: invalid number of arguments`            |
| Invalid key format            |  `InvalidKeyError: <reason>`                                |
| Value is not a number         |  `InvalidValueError: provided value is not a valid number`  |

***

#### **Use Cases**

* **Store User Balances**

  ```bash 
  NUM.SET user:1001:balance 123.45
  ```

* **Cache Calculated Values**

  ```bash 
  NUM.SET temperature:nyc 25.6
  ```

* **Replace Previous Values**

  ```bash 
  NUM.SET retry_count 5
  NUM.SET retry_count 6
  ```

* **Store Negative or Floating Values**

  ```bash 
  NUM.SET altitude -431.2
  ```

 
