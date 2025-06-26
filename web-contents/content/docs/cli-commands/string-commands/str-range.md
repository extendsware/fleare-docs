---
draft: false
title: STR.RANGE
is_title_visible: false
description: >-
  The STR.RANGE command returns a substring from a string value stored at a
  specified key
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline

date: '2025-06-19T18:06:26.611Z'
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
weight: 2000000
id: /documentations/cli-commands/string-commands/str-range.md
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T19:42:23.485Z'
---
#### Command: `STR.RANGE` 

***

#### Overview

The `STR.RANGE` command returns a **substring** from a string value stored at a specified key, based on **start** and **end offsets** (inclusive). It supports **negative indices**, enabling easy access to characters counted from the end of the string.

#### Command Name

 `STR.RANGE` 

***

#### Description

Fetches a substring from the string value at the given key. The command uses inclusive index ranges, with support for both **positive** and **negative** indexing.

*  `start` and `end` specify the beginning and end of the substring (inclusive of `start` , exclusive of `end + 1` ).

* **Negative offsets** count from the end of the string ( `-1` is the last character, `-2` the second last, etc.).

#### Use Cases

* Extracting a snippet from a large text or paragraph.
* Reusing substrings for further operations like `STR.SET` , `STR.APPEND` .
* Testing or validating specific parts of a stored string value.
* Implementing document-based or line-based inspection (e.g., logs, texts).

#### Syntax

```bash 
STR.RANGE <key> <start> <end>
```

*  `<key>` : The string key from which to extract the substring.

*  `<start>` : Starting offset (can be negative).

*  `<end>` : Ending offset (can be negative).

#### Permissions

* Requires **read access** to the key.

* No modification is performed; **safe for concurrent reads**.

***

#### Input Examples

##### Basic positive offsets

```bash 
localhost:9219> SET myKey "There are many variations of passages"

Ok

localhost:9219> STR.RANGE myKey 0 4

Ok "There"
```

##### Mixed positive and negative offsets

```bash 
localhost:9219> STR.RANGE myKey 15 -1

Ok "variations of passages"
```

##### Negative start index

```bash 
localhost:9219> STR.RANGE myKey -8 4

Ok "pass"
```

##### Start > End

```bash 
localhost:9219> STR.RANGE myKey 15 10

Ok "variations"
```

***

#### Output Examples

| Input Command             | Output                       |
| ------------------------- | ---------------------------- |
|  `STR.RANGE myKey 0 5`    |  `"There "`                  |
|  `STR.RANGE myKey 15 10`  |  `"variations"`              |
|  `STR.RANGE myKey -8 4`   |  `"pass"`                    |
|  `STR.RANGE myKey 15 -1`  |  `"variations of passages"`  |

***

#### Behavior on Error

| Condition                      | Error Message                                                     |
| ------------------------------ | ----------------------------------------------------------------- |
| Missing arguments              |  `InvalidKeyError: invalid number of arguments`                               |
| Key does not exist             |  `KeyNotFoundError: provided key does not exist`                               |
| Key exists but is not a string |  `InvalidValueError: the existing value for the provided key must be a string`  |         
| Non-integer start/end          |  `InvalidArgsError: start offsets must be valid integers`                      |



 
