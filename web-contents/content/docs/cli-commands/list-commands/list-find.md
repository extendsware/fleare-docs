---
draft: false
title: LIST.FIND
is_title_visible: false
description: >-
  The LIST.FIND command filters elements from a list stored at a specified key
  using various comparison operators and path-based expressions.

date: '2025-06-20T16:46:42.682Z'
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
id: /documentations/cli-commands/list-commands/list-filter.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.504Z'
---
#### Command: `LIST.FIND` 

***

#### Overview

The `LIST.FIND` command filters elements from a list stored at a specified key using various comparison operators and path-based expressions. It supports FIND primitives (strings, numbers, booleans) and objects (using nested field paths).

#### Description

Filters the list elements stored at a key based on a specified path filter expression.

* Works with lists containing primitives or objects.

* Supports filtering by value equality, inequality, case-insensitive matching, and numeric comparisons.

* Supports nested field access using dot notation (e.g., `$preferences.theme:dark` ).

#### Use Cases

* Retrieve only matching strings or numbers from a list.

* Filter out specific values.

* Extract objects where nested fields match a specific value.

* Use numeric and boolean comparisons in filter logic.

#### Syntax

```bash 
LIST.FIND <key> <path>
```

*  `<key>` : The list key to filter.

*  `<path>` : A filter expression used to match list items.

***

#### Filter Path Syntax

For primitive lists:

  * `:` <value>    — equals
  * `!` <value>    — not equals
  * `~` <value>    — case-insensitive equals
  * `>` <value>    — greater than
  * `<` <value>    — less than
  * `>=` <value>   — greater than or equal
  * `<=` <value>   — less than or equal

For object lists:
```css 
  $<field> : <value>        — field equals value 
  $<field> ! <value>        — field not equals value
  $<field> ~ <value>        — field case-insensitive match
  $<field> > <value>        — numeric comparison
  $<nested.field> : <value> — nested field match
```

***

#### Permissions

No special permissions required. Any user with access to the key can perform this operation.

***

#### Examples

##### LIST.FIND – Numeric Finding Examples

The following examples assume that you have a numeric list already stored using `LIST.SET`.

* Setup

```bash 
127.0.0.1:9219> LIST.SET myNum 10 20 30 40 50 60 70 80 90 100
Ok 10
```
###### 1. `:` (Equal to)

```bash 
127.0.0.1:9219> LIST.FIND myNum ':30'
Ok [30]
```

```bash 
127.0.0.1:9219> LIST.SET myFloats 10.5 20.0 30.3 40.0
Ok 4

127.0.0.1:9219> LIST.FIND myFloats ':40.0'
Ok [40.0]
```

###### 2. `!` (Not equal to)

```bash 
127.0.0.1:9219> LIST.FIND myNum '!60'
Ok [10,20,30,40,50,70,80,90,100]
```
###### 3. `>` (Greater than)

```bash 
127.0.0.1:9219> LIST.FIND myNum '>50'
Ok [60,70,80,90,100]
```
###### 4. `<` (Less than)

```bash 
127.0.0.1:9219> LIST.FIND myNum '<40'
Ok [10,20,30]
```
###### 5. `>=` (Greater than or equal to)

```bash 
127.0.0.1:9219> LIST.FIND myNum '>=70'
Ok [70,80,90,100]
```

###### 6. `<=` (Less than or equal to)

```bash 
127.0.0.1:9219> LIST.FIND myNum '<=30'
Ok [10,20,30]
```

###### 7. Mixed Float and Int Filtering

```bash 
127.0.0.1:9219> LIST.SET numMixed 5.5 10 15.5 20 25.0
Ok 5

127.0.0.1:9219> LIST.FIND numMixed '>=15.5'
Ok [15.5, 20, 25.0]
```

###### 8. Finding by Float Using Integer Input

```bash 
127.0.0.1:9219> LIST.FIND numMixed '>=10'
Ok [10, 15.5, 20, 25.0]
```

######9. Finding by Integer Using Float Input

```bash 
127.0.0.1:9219> LIST.FIND numMixed '<=10.0'
Ok [5.5, 10]
```

###### 10. Edge Case: No Match

```bash 
127.0.0.1:9219> LIST.FIND myNum '>1000'
Ok []
```

Here are **all possible string-based filter examples** for the `LIST.FIND` command, covering each supported string operator and its behavior:

---

##### String Filter Examples for `LIST.FIND`

Assume the list contains:

```bash 
127.0.0.1:9219> LIST.SET names "John" "Emily" "Michael" "john" "JANE" "jane" "Michael" "Robert"
Ok 8
```

###### 1. `:<value>` — **Equals (case-sensitive)**

Returns elements exactly equal to the given value.

```bash 
127.0.0.1:9219> LIST.FIND names ':John'
Ok ["John"]
```

###### 2. `!<value>` — **Not equals (case-sensitive)**

Returns elements not equal to the given value.

```bash 
127.0.0.1:9219> LIST.FIND names '!John'
Ok ["Emily","Michael","john","JANE","jane","Michael","Robert"]
```

##### 3. `~<value>` — **Case-insensitive match**

Returns elements that match the value, ignoring case.

```bash 
127.0.0.1:9219> LIST.FIND names '~john'
Ok ["John","john"]
```

```bash 
127.0.0.1:9219> LIST.FIND names '~jane'
Ok ["JANE","jane"]
```

---
##### String Filter Examples for `LIST.FIND`

###### `$<field>:<value>` — **String match on object fields**

Given a list of JSON objects:

```bash 
127.0.0.1:9219> LIST.PUSH users '{"name": "John", "role": "admin"}'
Ok 1
127.0.0.1:9219> LIST.PUSH users '{"name": "Emily", "role": "user"}'
Ok 2
127.0.0.1:9219> LIST.PUSH users '{"name": "john", "role": "admin"}'
Ok 3
```

###### Case-sensitive match:

```bash 
127.0.0.1:9219> LIST.FIND users '$name:John'
Ok [{"name":"John","role":"admin"}]
```

###### Case-insensitive match:

```json 
127.0.0.1:9219> LIST.FIND users '$name~john'
Ok [
  { "name": "John", "role": "admin" },
  { "name": "john", "role": "admin" }
]
```

###### Not equals:

```bash 
127.0.0.1:9219> LIST.FIND users '$role!admin'
Ok [{"name":"Emily","role":"user"}]
```

---

###### `$<nested.field>:<value>` — **Nested field match**

```bash 
127.0.0.1:9219> LIST.PUSH accounts '{"user": {"name": "John", "role": "admin"}}'
127.0.0.1:9219> LIST.PUSH accounts '{"user": {"name": "Emily", "role": "user"}}'
127.0.0.1:9219> LIST.PUSH accounts '{"user": {"name": "john", "role": "admin"}}'
```

###### Match exact:

```json 
127.0.0.1:9219> LIST.FIND accounts '$user.name:John'
Ok [{ "user": { "name": "John", "role": "admin" } }]
```

###### Case-insensitive:

```json 
127.0.0.1:9219> LIST.FIND accounts '$user.name~john'
Ok [
  { "user": { "name": "John", "role": "admin" } },
  { "user": { "name": "john", "role": "admin" } }
]
```

###### Invalid path (field doesn't exist):

```bash 
127.0.0.1:9219> LIST.FIND names '$nonexistent:value'
Ok []
```

##### Non-string types with string operator:

```bash 
127.0.0.1:9219> LIST.SET mixed 1 true "true" "false" false
Ok 5

127.0.0.1:9219> LIST.FIND mixed ':true'
Ok ["true"]
```

***

#### Behavior on Error

| Scenario                              | Error Message                                                                            |
| ------------------------------------- | ---------------------------------------------------------------------------------------- |
| Missing key                           |  `InvalidKeyError: Key must be provided`                                                 |
| Wrong number of arguments             |  `InvalidArgsError: invalid number of arguments, Syntax: LIST.FIND <key> <path>`       |
| Non-list value                        |  `InvalidValueError: The current value associated with the provided key must be a list`  |
| Invalid JSON or corrupted data        |  `InvalidCharacterError: <underlying error>`                                             |
| Filter path references missing fields | Returns an empty array                                                                   |

 
