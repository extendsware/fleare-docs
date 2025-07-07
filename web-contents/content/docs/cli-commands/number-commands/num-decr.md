---
draft: false
title: NUM.DECR
is_title_visible: false
description: >-
  The NUM.DECR command decrements the numeric value stored at the specified key
  by a given amount.

date: '2025-06-20T10:56:54.541Z'
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
id: /documentations/cli-commands/number-commands/num-decr.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.473Z'
---
#### Command: `NUM.DECR` 

***

#### Overview

The `NUM.DECR` command decrements the numeric value stored at the specified key by a given amount. If the key does not exist, it initializes the key with the decremented value (i.e., `0 - value` ). If no amount is provided, it decrements by 1 by default.

#### Command Name

 `NUM.DECR` 

***

#### Description

This command is used to decrement a stored numeric value.

* If the key exists and holds a valid number, the command subtracts the specified value from it.

* If the key does not exist, it will create the key with the result of `0 - value` .

* If the value provided is not a number or the existing value is not numeric, the command will return an error.

* Supports both integers and floating-point numbers.

#### Use Cases

* **Decrement counters**: Decrease a numeric counter by a fixed amount (e.g., tracking retries or remaining attempts).

* **Countdown timers**: Gradually reduce a floating-point timer value.

* **Credit/balance management**: Subtract units from a user’s balance or quota.

* **Initialization with negative values**: Auto-create keys with negative values if not already present.

#### Syntax

```bash 
NUM.DECR <key> [value]
```

*  `<key>` : Required. The key whose value you want to decrement.

*  `[value]` : Optional. The numeric value to decrement by (defaults to `1` if omitted).

***

#### Permissions

* Read/Write access to the specified key.

* Append permission for the Write-Ahead Log (WAL).

***

#### Input Examples

##### Example 1: Decrement existing number by 1

```bash 
localhost:9219> NUM.SET myNumber 42
Ok

localhost:9219> NUM.DECR myNumber
Ok 41
```

##### Example 2: Decrement existing number by a specific amount

```bash 
localhost:9219> NUM.SET myNumber 42
Ok
localhost:9219> NUM.DECR myNumber 10
Ok 32
```

##### Example 3: Decrement a float value

```bash 
localhost:9219> NUM.SET myNumber 11.5
Ok
localhost:9219> NUM.DECR myNumber
Ok 10.5
localhost:9219> NUM.DECR myNumber 0.5
Ok 10
```

##### Example 4: Decrement a non-existent key

```bash 
localhost:9219> NUM.DECR myNewKey 5
Ok -5
```

***

#### Output Examples

* If successful, returns the new value:

  ```bash 
  Ok 41
  ```

* If a float is involved:

  ```bash 
  Ok 10.5
  ```

* For a non-existent key:

  ```bash 
  Ok -5
  ```

***

#### Behavior on Error

The following errors can occur:

| Condition                               | Error Message                                                                   |
| --------------------------------------- | ------------------------------------------------------------------------------- |
| Missing key argument                    |  `InvalidKeyError: Key must be provided`                                        |
| More than two arguments                 |  `InvalidArgsError: invalid number of arguments`                                |
| Invalid key format                      |  `InvalidKeyError: <error details>`                                             |
| Non-numeric input value                 |  `InvalidValueError: provided value is not a valid number`                      |
| Existing key has non-numeric value type |  `InvalidValueError: the existing value for the provided key must be a number`  |

 
