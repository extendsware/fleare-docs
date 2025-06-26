---
draft: false
title: GET
is_title_visible: false
description: >-
  The GET command retrieves the value associated with a given key from the
  in-memory database.
cover_image: >-
  https://www.bakemyweb.com/files/public/82/88/6857019939714a001e078288/i/5c/5e/685701b8a14834001f8a5c5e/original?name=logo-large.png&mimetype=image/png&cd=inline
date: '2025-06-21T20:21:24.597Z'
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
id: /documentations/cli-commands/get.md
weight: 5000000
__system:
  created_by: i-602132207af9e10032069067
  new: false
  last_published: '2025-06-21T20:35:27.652Z'
---
#### Command: `GET` 

***

#### Overview

The `GET` command retrieves the value associated with a given key from the in-memory database. If the value is a nested JSON object, an optional path can be provided to extract specific nested fields.

#### Command Name

 `GET` 

#### Description

Fetches the value associated with a key. If the value is a JSON object or structure, you can extract a specific field using a dot-notated path (e.g., `user.name.first` ).

#### Use Cases

* Retrieve a primitive or complex value stored against a key.

* Extract a specific field from a nested JSON object.

* Validate the existence or contents of a key.

#### Syntax

```bash 
GET <key> [<path>]
```

*  `<key>` : The required key name.

*  `<path>` *(optional)*: Dot-separated string to retrieve a nested field from a JSON object.

#### Permissions

* No authentication is required to use `GET` .

* The user must have **read** access if ACL or user roles are enforced (future extension).

***

#### Examples

##### Example 1: Fetching a Simple Value

```bash 
localhost:9219> GET user:1
{"name":"John Doe","age":30}
```

##### Example 2: Fetching a Nested Value from JSON

```bash 
localhost:9219> GET user:1 name
"John Doe"
```

##### Example 3: Fetching Deeply Nested Value

Stored value:

```json 
{
  "user": {
    "profile": {
      "email": "john@example.com"
    }
  }
}
```

```bash 
localhost:9219> GET user:1 user.profile.email
"john@example.com"
```

##### Example 4: Missing Key

```bash 
localhost:9219> GET non_existing_key
(empty response)
```

***

#### Behavior on Error

| Scenario                        | Error Message                                     |
| ------------------------------- | ------------------------------------------------- |
| Key not provided                |  `ERR invalid key: Key must be provided`          |
| Too many arguments              |  `ERR invalid args: invalid number of arguments`  |
| Invalid key format              |  `ERR invalid key: <reason>`                      |
| Invalid path or non-JSON value  |  `ERR invalid character: <JSON error>`            |
| Path not found in nested object |  `ERR key not found: <missing key>`               |
| Path points to non-object value |  `ERR invalid path: <full path>`                  |

***

#### Notes

* Dot notation supports any depth (e.g., `a.b.c.d` ).

 
